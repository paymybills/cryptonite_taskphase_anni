# Efficient Key Exchange - CTF Writeup

## Problem Overview

In this challenge, we are tasked with calculating the shared secret from Alice's public key, but only the x-coordinate of Alice's public key is given. We are not directly provided with the y-coordinate, but we are given a set of hints that will help us derive it. The key hint provided is that the prime \( p \) satisfies the condition \( p \equiv 3 \mod 4 \), which will be crucial in determining the correct \( y \)-coordinate.

## Approach

### 1. Understanding the Weierstrass Equation

The elliptic curve equation used for key exchange follows the Weierstrass equation:

\[
y^2 = x^3 + ax + b \mod p
\]

In this case, we are provided with the x-coordinate \( x = 815 \) and the corresponding \( y = 3190 \), but the actual value of \( y \) is hidden. The task is to calculate \( y \) from this x-coordinate using the hints and the Weierstrass equation.

### 2. Computing \( y^2 \)

First, we substitute the given \( x = 815 \) into the Weierstrass equation to compute \( y^2 \mod p \). This gives us a value that will allow us to compute the possible values for \( y \).

### 3. Calculating Possible y-Values

To calculate the corresponding \( y \)-values, we need to find the square roots of \( y^2 \) modulo \( p \). This involves checking all possible values \( i \) such that:

\[
i^2 \equiv y^2 \mod p
\]

The following Python function is used to find the two possible values of \( y \):

```python
def sqrt(ysq, p):
    for i in range(1, p):
        if pow(i, 2, p) == ysq:
            return (i, p - i)
```
After running this function, we obtain two potential values for yy: y1=3452y1​=3452 and y2=6287y2​=6287.
4. Determining the Correct y-Coordinate

To determine which of the two possible values of yy is the correct one, we use the hint that p≡3mod  4p≡3mod4. The correct yy-coordinate is the one that satisfies the condition ymod  4=3ymod4=3.

We check both values:

    For y1=3452y1​=3452, we compute 3452mod  43452mod4, which does not give 3.
    For y2=6287y2​=6287, we compute 6287mod  46287mod4, which results in 3, thus satisfying the condition.

Therefore, y2=6287y2​=6287 is chosen as the correct yy-coordinate for Alice’s public key.
5. Calculating the Shared Secret

With the correct yy-coordinate determined, we now compute the shared secret. The shared secret is calculated using the Diffie-Hellman method:
shared_secret=pow(A,b,p)
shared_secret=pow(A,b,p)

where AA is Alice's public key (given by the x- and y-coordinates), and bb is your private key (as the attacker or participant in the legitimate exchange).
6. Decrypting the Flag

With the shared secret in hand, we provide the x-coordinate of Alice's public key, along with the IV and ciphertext, to the decryption script (decrypt.py). The decryption script uses the shared secret to decrypt the flag.
Flag

After completing the key exchange and decryption process, we obtain the following flag:

crypto{3ff1c1ent_k3y_3xch4ng3}

Conclusion

This challenge involved applying elliptic curve cryptography principles, specifically focusing on deriving the hidden y-coordinate using modular arithmetic and the Weierstrass equation. By using the provided hint p≡3mod  4p≡3mod4, we efficiently determined the correct y-coordinate and computed the shared secret, which allowed us to decrypt the final flag.
