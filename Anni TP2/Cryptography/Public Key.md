---

# Public Key

Again, make vairables, make formulae
```python
# Given values for RSA encryption
message = 12
e = 65537
p = 17
q = 23
N = p * q  # Modulus N = p * q

# Performing modular exponentiation for encryption: ciphertext = message^e mod N
ciphertext = pow(message, e, N)
ciphertext  # Result: 301
```

The ciphertext obtained by encrypting the number `12` using `e = 65537`, `p = 17`, and `q = 23` is `301`.

