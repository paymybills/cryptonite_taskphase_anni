# Spelling Quiz

"I found the flag, but my brother wrote a program to encrypt all his text files. He has a spelling quiz study guide too, but I don't know if that helps."

```python
import random
import os

files = [
    os.path.join(path, file)
    for path, dirs, files in os.walk('.')
    for file in files
    if file.split('.')[-1] == 'txt'
]

alphabet = list('abcdefghijklmnopqrstuvwxyz')
random.shuffle(shuffled := alphabet[:])
dictionary = dict(zip(alphabet, shuffled))

for filename in files:
    text = open(filename, 'r').read()
    encrypted = ''.join([
        dictionary[c]
        if c in dictionary else c
        for c in text
    ])
    open(filename, 'w').write(encrypted)
```

Flag:

brcfxba_vfr_mid_hosbrm_iprc_exa_hoav_vwcrm

study-guide.txt:

└─$ cat public/study-guide.txt | head
hxqfbwfwgh
yzlmhzxpq
eqhhgrhzqf
dzjfwxfqs
lwfpqwgpwt
iwgtwfzfpqs
xfpfmqppyx
mlwgthqxwz
twxzeqhhzdwlwfs
mqprlwfr

└─$ wc -l public/study-guide.txt
272543 public/study-guide.txt

So it's a substitution cipher. Basically, it searches for .txt files, creates an alphabet list, shuffles the copy, creates a random cipher, and makes a dictionary.

Using CrypTool: pasted the first few lines, then Analysis → Frequency → Alphabetic

or

Analysis → Automatic Analysis → Known Ciphertext Only → Mono sub

The flag: `picoCTF{perhaps_the_dog_jumped_over_was_just_tired}`

## Scrambled RSA

n and e are given. Encrypting "hello" gives different characters every time - non-deterministic.

Encrypt partial prefix of the text. I tried h, he, hel, and so forth, but then I realized it's moot, so I did p, pi, pico, something.

Check if E(p), E(pi)… is present in the flag (didn't work, by the way).

Now a big problem is removing noise. I looked up how to remove noise from a non-deterministic encryption.

Suppose E(abc) exists, ⇒ E(a), E(b), E(c) make up the original. Here we need to identify the original by input comparison, so encrypt characters, then substring, mix and match.

```python
from Crypto.Util.number import long_to_bytes, bytes_to_long
import string

# Constants

N = 106393877387061674780269443416122033957470775377538503986525156853344106645258943831036053499392577287359309204310519147714363669430556595918051924362857879883648386846033045170831033578612419189879345630099664288981304224208850344812969488431038558262641627552457836197084966102117701680185682779525658336377
E = 65537
CHARSET = string.ascii_lowercase + string.digits + '_}'

# Functions

def encrypt(msg):
    return pow(bytes_to_long(msg.encode()), E, N)

def try_decrypt(encrypted_flag):
    flag = "picoCTF{"
    while "}" not in flag:
        for c in CHARSET:
            test = flag + c
            if encrypt(test) == encrypted_flag:
                flag = test
                print(f"Found: {flag}")
                break
    return flag

# Main

if __name__ == "__main__":
    test_flag = encrypt("picoCTF{t}")
    recovered = try_decrypt(test_flag)
    print(f"Final flag: {recovered}")
```

## SRA

No hint given. nc [saturn.picoctf.net](http://saturn.picoctf.net) 60300, then downloaded [chal.py](http://chal.py)

```python
from Crypto.Util.number import getPrime, inverse, bytes_to_long
from string import ascii_letters, digits
from random import choice

pride = "".join(choice(ascii_letters + digits) for _ in range(16))
gluttony = getPrime(128) # p
greed = getPrime(128) #    q
lust = gluttony * greed #  n
sloth = 65537 #            e
envy = inverse(sloth, (gluttony - 1) * (greed - 1)) # d

anger = pow(bytes_to_long(pride.encode()), sloth, lust)

print(f"{anger = }")
print(f"{envy = }")

print("vainglory?")
vainglory = input("> ").strip()

if vainglory == pride:
    print("Conquered!")
    with open("/challenge/flag.txt") as f:
        print(f.read())
else:
    print("Hubris!")
```

We need n.

e and d are given.

e·d ≡ 1 (mod φ(N)), φ(n) = (p-1)(q-1)

Asked GPT to write code for it.
It spat out:

```python
factors_string = '2^6 × 3^2 × 5 × 587 × 24329 × 129631 × 407807 × 80787 180953 × 1241 605438 156271 × 84761 673627 946307 × 99817 949863 851199'
factors = []
for factor in factors_string.split(' × '):
    factor = factor.replace(' ', '').strip()
    if '^' in factor:
        factor = factor.split('^')
        factors += [int(factor[0])] * int(factor[1])
    else:
        factors.append(int(factor))

factors = sorted(factors, reverse=True)
print(factors)
```

Was stuck, very, very stuck.

I realized that my approach of factorization of a large product was kind of stupid. Reverse Engineering p and q was going to be tough, slow, and complete factorization beforehand could not always be feasible.

### Instead, we do search and combination

We check for divisions of d·e congruent to 1 mod(φ b) ⇒ d·e - 1, generate divisions of this, hit and trials for p-1, q-1 for 128-bit primes, still dependent on ed-1 though.

Yet...

```python
from Crypto.Util.number import isPrime, long_to_bytes
from sympy import divisors
from itertools import combinations
from string import ascii_letters, digits
from math import log2

# Given values
anger = int(input("anger:"))  
envy = int(input("envy:"))    
sloth = 65537

# Calculate ed - 1
ed_minus_1 = envy * sloth - 1

# Get all divisors of ed - 1
divs = divisors(ed_minus_1)

# Filter potential primes: p - 1 and q - 1 must be divisors
primes = [d + 1 for d in divs if isPrime(d + 1)]

# Filter primes that are approximately 128 bits long (127-128 bits)
valid_primes = [p for p in primes if 127 <= log2(p) <= 128]

# Prepare to test combinations of primes
valid_plaintexts = []
charset = ascii_letters + digits  # Allowed characters in plaintext

# Test combinations of valid primes to reconstruct n = p * q
for p, q in combinations(valid_primes, 2):
    n = p * q  # Calculate n
    try:
        # Attempt decryption
        decrypted = long_to_bytes(pow(anger, envy, n)).decode('ascii')

        # Check if the decrypted plaintext matches the allowed character set
        if all(c in charset for c in decrypted):
            valid_plaintexts.append(decrypted)  # Store valid plaintext
    except Exception:
        continue  # Skip invalid combinations

# Print results
if valid_plaintexts:
    print("Possible plaintexts:", valid_plaintexts)
else:
    print("No valid plaintexts found.")
```

## Sum-o-primes

First, download [gen.py](http://gen.py) and output.txt

```python
#!/usr/bin/python

from binascii import hexlify, unhexlify
from gmpy2 import mpz_urandomb, next_prime, random_state
import math
import os
import sys

if sys.version_info < (3,):
    math.gcd = gmpy2.gcd
    math.lcm = gmpy2.lcm

FLAG = open('flag.txt').read().strip()
FLAG = int(hexlify(FLAG.encode()), 16)
SEED = int(hexlify(os.urandom(32)).decode(), 16)
STATE = random_state(SEED)

def get_prime(bits):
    return next_prime(mpz_urandomb(STATE, bits) | (1 << (bits - 1)))

p = get_prime(1024)
q = get_prime(1024)
x = p + q
n = p * q
e = 65537
m = math.lcm(p - 1, q - 1)
d = pow(e, -1, m)
c = pow(FLAG, e, n)

print(f'x = {x:x}')
print(f'n = {n:x}')
print(f'c = {c:x}')
```

N is p·q, C is message, x is variable.

Output has a lot more content, but it's in hex. Convert it online.

Decipher c, get flag.

We know p + q = n.

p · q = x

Make quadratic, solve it, get p,q, e = 65537, d = e^(-1) mod(p-1·q-1)

Then decrypt.

Here's what GPT spat out:

```python
import math

# Parse input values
x = int((Lines[0].split())[2], 16)  # x = p + q (sum of primes)
n = int((Lines[1].split())[2], 16)  # n = p * q (product of primes)
c = int((Lines[2].split())[2], 16)  # c = ciphertext

def solve_rsa_primes(sum_pq: int, prod_pq: int) -> tuple:
    """
    Solve RSA prime numbers (p, q) using the quadratic equation:
    p^2 - sum_pq * p + prod_pq = 0

    Formula used:
    p = (sum_pq / 2) ± sqrt((sum_pq / 2)^2 - prod_pq)

    Args:
        sum_pq (int): Sum of the primes (p + q).
        prod_pq (int): Product of the primes (p * q).

    Returns:
        tuple: The two prime numbers (p, q).
    """
    # Calculate half of the sum
    half_sum = sum_pq // 2

    # Compute the discriminant for the quadratic formula
    discriminant = math.isqrt(half_sum ** 2 - prod_pq)

    # Solve for p and q
    p = half_sum + discriminant
    q = half_sum - discriminant

    return int(p), int(q)

# Calculate p and q
p, q = solve_rsa_primes(x, n)

# Compute Euler's Totient Function (phi) using LCM
phi_n = math.lcm(p - 1, q - 1)

# RSA public and private keys
e = 65537  # Public exponent
d = pow(e, -1, phi_n)  # Private exponent

# Decrypt the ciphertext
FLAG = pow(c, d, n)

# Convert the decrypted integer to bytes and print the flag
print(FLAG.to_bytes((FLAG.bit_length() + 7) // 8, 'big').decode())
```

## No padding, no problem or summet:

**Padding** is the process of adding extra data to a plaintext message before encrypting it. This ensures that the message conforms to a required format or size, making the encryption more **secure** and resistant to attacks.
It's kind of similar to ML.

You need it because some AES and all need the text to be a multiple of a specific block size, and it also prevents patterns.

Oracle is sort of a feedback on correctness of data.

### Padding attack on oracle, so the oracle checks whether the decrypted message is valid or not.

Decrypt without knowing key. 

### CBC each plaintext is XORed with previous cipher block, so sort of a previous step based process.

Now for the attack itself, if you capture an encrypted message, an error message can be flashed from the oracle( the server itself), the server will let them know if cipher is right or wrong. so the attack is essentially looping every bite from 0-255, until padding is correct.

if correct, then reverse XOR it back and back until plaintext is reached

then last byte → second last→ on and on

## Can be mitigated by no padding

# Solution for NO Padding No Proble

Nc to server

Oracle gives me (n ,e) and c. 

Seems rather stupid to not take the no padding in consideration so here’s what i’m gonna do. Homomorphic attack ( property is that E(m1).E(m2) mod n = E(m1.m2)

So if  I have C= E(m) then we encrypt x and compute C’= C.E(x). Now if I submit C’, the oracle will decrypt m.x and dividing out x, attacker will give me m. More of a math property exploitation . (Bleichenbacher’s )

In Bleich, we reconstruct the shit bit by bit.

In this case what we do is, we have unpaded rsa

I’ll take variable x as 2 (because taking 1 is stupid)

now we’ll encrypt it using 2^e mod n= X

then we’ll multiply our ciphertext and x so that when we give it to the oracle, it spits out m*2. 

now we decrypt it by feeding it to the oracle. 

“Here you go” received

divide the received by 2

we have n. 

now hex decode it 

# Bonus RSA 1

```python
from Crypto.Util.number import *

m = open("flag.txt",'rb').read()

m = bytes_to_long(m)

p = getPrime(1024)
q = getPrime(1024)
N = p*q

e = getRandomNBitInteger(16)
c = pow(m,e,N)
p_ = p >> (200)

print(f"{(p_,N,e,c)=}")

# (p_,N,e,c)=(78251056776113743922781362749830646373211175353656790171039496888342171662458492506297767981353887690931452440620588460424832375197427124943346919084717792877241717599798699596252163346397300952154047511640741738581061446499402444306089020012841936, 19155750974833741583193175954281590563726157170945198297004159460941099410928572559396586603869227741976115617781677050055003534675899765832064973073604801444516483333718433505641277789211533814981212445466591143787572063072012686620553662750418892611152219385262027111838502078590253300365603090810554529475615741997879081475539139083909537636187870144455396293865731172472266214152364966965486064463013169673277547545796210067912520397619279792527485993120983571116599728179232502586378026362114554073310185828511219212318935521752030577150436386831635283297669979721206705401841108223134880706200280776161816742511, 37929, 18360638515927091408323573987243771860358592808066239563037326262998090628041137663795836701638491309626921654806176147983008835235564144131508890188032718841579547621056841653365205374032922110171259908854680569139265494330638365871014755623899496058107812891247359641915061447326195936351276776429612672651699554362477232678286997748513921174452554559807152644265886002820939933142395032126999791934865013547916035484742277215894738953606577594559190553807625082545082802319669474061085974345302655680800297032801212853412563127910754108599054834023083534207306068106714093193341748990945064417347044638122445194693)
```

I'm given basically p_ (a partial prime).

(A partial prime (p_) in this context is a portion of the original prime number p that has been right-shifted by 200 bits, as shown by the operation `p_ = p &gt;&gt; (200)`. This means we only have access to the most significant bits of p, with the last 200 bits being removed.

In the code, this is demonstrated by the line `p_ = p &gt;&gt; (200)`, where >> is the right shift operator that effectively divides p by 2^200, giving us only the upper bits of the original prime.)

E is random.

c ≡ m^e (mod N)

So we can see p_ is leaked, so p can be maybe reconstructed? p = p' + x

Looking it up, it's called a small root problem: you have f(x) and N, find x such that f(x) ≡ 0 (mod n), where x is small.

Solved using coppersmith, used when MSB or LSB is leaked (given here).
We'll create N = (p' + x) * q       (n = p*q)

This gives us:

f(x) = (p' + x)(q) - N

Since x is small, we can treat it as f(x) modulo N.

We use LLL algo, basically forms a lattice of all integer combinations, sort of a grid. Now the lattice basis is input, output is reduced basis, where basis vectors are shorter and orthogonal.

We do gram schmidt and then RRER. Lovasz condition idk, then swap and recompute until basis is reduced. Now I have the shortest vectors.

How does this work in this case?
I took multiple shifted polynomials by multiplying it with x and N raised to something, formed a lattice, then used LLL, which contains the short vectors and by the virtue of it being RRERed, the vectors are linked.

From here it's easy, we find x₀ using gcd or something.

Key idea is LLL corresponds to polynomials with small coefficients which will vanish at root x₀. The polynomials encode the modular relation f(x₀) ≡ 0.

So we have f(x) = (p₀ + x)q - N, construct lattice, short vectors in reduced form reveal a polynomial whose root corresponds to x.
Now we have x, p = p₀ + x, q = N/p

Now we have p and q instead of partials.

φ(n) = (p-1)(q-1), get d from e⁻¹ mod φ(n) then decrypt

Using m ≡ c^d (mod n)

## Basically:

- **Define Polynomial**:
    - f(x)=(p′+x)q−Nf(x) = (p' + x)q - Nf(x)=(p′+x)q−N with p′ as partial prime p.
        
        p′p'
        
        pp
        
    - The lattice is constructed using polynomials shifted and scaled by powers of N.
        
        NN
        
- **Lattice Construction**:
    - A matrix representing shifted and scaled forms of the polynomial is constructed.
    - Diagonal entries are scaled by N to ensure integer entries.
        
        
- **LLL Reduction**:
    - The LLL algorithm reduces the lattice basis.
    - Resulting vectors encode small-coefficient polynomials.
- **Extract Short Vector**:
    - The reduced basis reveals a polynomial that vanishes at x0​ (the small root).
        
        
- **Recover Full Prime**:
    - Combine p′ and x0 to compute p.
    - Use N=pq to compute q.

N=pqN = pq

- **Decrypt**:
    - Compute ϕ(N), derive d, and decrypt c to retrieve the plaintext.
        
        ϕ(N)\phi(N)
        

# Bonus 2 Meta flippy #unsolved

I can see in this ruby code that I have basically

```ruby
#!/usr/local/bin/ruby

require 'openssl'
require 'io/console'
$stdout.sync = true

FLAG = ENV['FLAG'] || 'MetaCTF{test_flag}'

  def generate_random_key
    OpenSSL::Cipher.new('AES-128-CBC').random_key
  end

  def encrypt(msg, key)
    cipher = OpenSSL::Cipher.new('AES-128-CBC')
    cipher.encrypt
    iv = cipher.random_iv
    cipher.key = key
    encrypted = cipher.update(msg) + cipher.final
    iv + encrypted
  end

  def decrypt(ct, key)
    decipher = OpenSSL::Cipher.new('AES-128-CBC')
    decipher.decrypt
    decipher.key = key
    iv = ct[0..15]
    encrypted_msg = ct[16..-1]
    decipher.iv = iv
    decipher.update(encrypted_msg) + decipher.final
  end

def main
  key = generate_random_key

  while true
    puts '1. Request print command'
    puts '2. Execute print command'
    print '> '
    choice = STDIN.gets.chomp

    case choice.strip
    when '1'
      print 'Enter a message: '
      msg = STDIN.gets.chomp
      if !msg.match(/\A[a-zA-Z0-9\.!]*\Z/)
        puts 'Invalid message!'
      else
        encrypted_msg = encrypt("puts '#{msg}'", key)
        puts "Encrypted message: #{encrypted_msg.unpack('H*')[0]}"
      end
    when '2'
      print 'Enter an encrypted command (hex): '
      enc_cmd = STDIN.gets.chomp
      cmd = decrypt([enc_cmd].pack('H*'), key)
      eval cmd
    else
      puts 'Invalid choice.'
    end
  end
end

main

```

- **Global Variable**:
    - `FLAG`: This variable holds a flag value, which is either taken from the environment variable `FLAG` or defaults to `'MetaCTF{test_flag}'`.
- **Functions**:
    - `generate_random_key`: This function generates a random key for AES-128-CBC encryption.
    - `encrypt(msg, key)`: This function encrypts a given
    message using the provided key. It creates a new cipher, generates a
    random initialization vector (IV), and returns the IV concatenated with
    the encrypted message.
    - `decrypt(ct, key)`: This function decrypts a given
    ciphertext using the provided key. It extracts the IV from the beginning of the ciphertext, sets it in the cipher, and then decrypts the rest of the message

The user is prompted to enter a message. If the message contains only 
allowed characters (alphanumeric and some punctuation), it encrypts the 
message using the `encrypt` function and displays the encrypted message in hexadecimal format.

Looking at it, the potential exploits could be to either craft a message that, when decrypted, executes arbitrary code…. or it could to use puts

So I could have 

puts FLAG

then encrypt this using AES 128 CBC, giving me ciphertext, then convert to hexadecc and input it to the script when prompt comes up. 
now upon decryption, puts FLAG is executed, revealing the flag. But I mean it only works when  I know the key and that’s stupid. It’s basically creating a new ciphertext from scratch and knowing the key at the time inside the main loop.

SO AFTER A LONG TIME, I looked it up online and a method to solve this would be BIT-Flipping 

So this is how it works,

The server CBC with random keys and IVs

and whatever command you prove,  it wraps in the 

puts  ‘input here’

template

then the decryption happens use eval cmd

GOAL HERE IS TO MANIPULATE OR TWEAK IT ENOUGH SO WE GET

puts FLAG

puts part is hard coded

now comes CBC malleability

in CBC, each block is XORed with the previous block 

so this gives me 

plaintext = Decrypt(Ciphertext) XOR IV

so if we modify IV, we can change the first block of plaintext.

we send in a sample message abcdefgh

then modify abcdefgh → FLAG

So what i think we should be doing here is 

abcdefgh 

and the server should respond with 

IV+ Ciphertext

so we calculate the XOR difference bit by bit between current plaintext and target plain text

Then we modify IV, such that when decrypted the plaintext matches our target

then we send new_iv+ cupher 

Can’t really test it so  that’s the modus operandi 

Basically

Encrypt stance is :

1. Divide plaintext in 16 bytes
2. XOR eaach block with IV (initial vector)
3. Encrypt 

- First Block:
C1​=E(P1​⊕IV)
- Second Block:
C2=E(P2⊕C1)
- Third Block:
C3​=E(P3​⊕C2​)

So if we modify IV< we can directly change without needing the key

now let our P= ‘puts flag’

IV provided by server

D(C)⊕IV=′putsabcdefgh′

Diff = abcdefgh xor flag

new iv = iv xor diff

send modified iv 

[niteCTF breakdown ](https://www.notion.so/niteCTF-breakdown-175e27b7e81080319840e8762ef402cd?pvs=21)
