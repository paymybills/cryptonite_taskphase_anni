
## RSAabc Challenge

### Description

The "RSAabc" challenge required breaking a multi-layered cryptographic puzzle. The task combined techniques inspired by RSA encryption and other manipulations to obscure a flag hidden in the provided files: 

- `cipher.py`: A Python script implementing the encryption process.
- `out.txt`: The encrypted output.

The clue, "flip out," suggested reversing encryption steps or utilizing modular arithmetic, often used in RSA-like schemes.

---

### Approach

The encryption process depended on whether the ASCII value of each character in the plaintext was a prime number:

1. **Non-prime characters**:
   - ASCII values were encrypted using RSA.
   - The reversed plaintext characters were included in the output.

2. **Prime characters**:
   - Characters were converted to their Greek counterparts.
   - RSA encryption followed by a "googly" transformation was applied.

Steps to decrypt:

1. **Data Parsing**:
   - Split `out.txt` into components:
     - Extract characters into `greek.txt`.
     - Extract cipher texts into `cipher.txt`.
     - Extract modulus values into `modulus.txt`.

2. **Handle Non-prime Characters**:
   - Removed non-prime characters (English letters) from `greek.txt`, `cipher.txt`, and `modulus.txt`.
   - Retained indices for later use.

3. **Reverse RSA Encryption**:
   - Factored `n` values to obtain `p` and `q`.
   - Computed the private key \(d = e^{-1} \mod \phi(n)\).
   - Decrypted ciphertexts using RSA decryption:
     \[
     m = c^d \mod n
     \]

4. **Character Transformation**:
   - Applied reverse alphabet transformations for English letters.
   - Converted Greek characters back to English using a predefined mapping.

5. **Reconstruct the Message**:
   - Combined the results from prime and non-prime character decryption to reveal the flag.

---

### Key Functions and Code Snippets

#### Data Extraction

```python
def extract_data_from_outfile(input_file, greek_file, cipher_file, modulus_file):
    with open(input_file, 'r') as f:
        data = f.read()
    parts = data.split("ct:")
    characters = parts[0].strip()
    ct_part = parts[1].split("n:")[0].strip()
    n_part = parts[1].split("n:")[1].strip()
    ct_numbers = [int(num.strip()) for num in ct_part.split(',') if num.strip().isdigit()]
    n_numbers = [int(num.strip()) for num in n_part.split(',') if num.strip().isdigit()]
    with open(greek_file, 'w', encoding='utf-8') as f:
        f.write(characters)
    with open(cipher_file, 'w') as f:
        f.write(' '.join(map(str, ct_numbers)))
    with open(modulus_file, 'w') as f:
        f.write(' '.join(map(str, n_numbers)))
```

#### Prime Character Processing

```python
def get_pq_for_n(n):
    factors = sp.factorint(n)
    return list(factors.keys())

def compute_d(e, p, q):
    phi_n = (p - 1) * (q - 1)
    return sp.mod_inverse(e, phi_n)

def rsa_decrypt(ciphertext, n, d):
    return pow(ciphertext, d, n)
```

#### Reverse Transformations

```python
def reverse_alphabet(char):
    if char.isupper():
        return chr(155 - ord(char))
    elif char.islower():
        return chr(219 - ord(char))
    else:
        return char
```

---

### Results

Using these techniques, the encrypted data was decrypted successfully. The recovered flag was assembled by combining the processed data from both prime and non-prime cases.
nite{quICklY_grab_the_codE5_sgOqkA}

---
