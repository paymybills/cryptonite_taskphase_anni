### 1. Intercepting Alice's Public Parameters

Alice sends her Diffie-Hellman parameters to Bob, which include:
- A large prime \( p \)
- A generator \( g \)
- Alice’s public key \( A \), computed as:
  \[
  A = g^a \mod p
  \]
  where \( a \) is Alice's private key.

These parameters are intercepted and passed on unchanged to Bob.

---

### 2. Bob Computes His Public Key

Bob generates his private key \( b \) and computes his public key \( B \) using:
\[
B = g^b \mod p
\]
where \( b \) is Bob's private key.

---

### 3. Generating My Public Key as the Attacker (Man-in-the-Middle)

As the attacker (Mallory), I now generate my own private key \( b_{\text{mine}} \). In this case, I choose \( b_{\text{mine}} = 3 \) and compute my public key \( B_{\text{mine}} \) as:
\[
B_{\text{mine}} = g^{b_{\text{mine}}} \mod p = 2^3 \mod p = 8
\]
where \( g = 2 \) and \( p \) is the large prime Alice and Bob are using.

I then send \( B_{\text{mine}} = 8 \) to Alice, pretending to be Bob.

---

### 4. Alice Computes the Shared Secret

Alice now uses \( B_{\text{mine}} \) (which she believes is Bob's public key) to compute the shared secret using her private key \( a \). The shared secret \( ss_{\text{alice}} \) is computed as:
\[
ss_{\text{alice}} = B_{\text{mine}}^a \mod p = 8^a \mod p
\]
This gives Alice a shared secret, which she will use to encrypt her messages to Bob.

---

### 5. Computing the Same Shared Secret as Alice

As the attacker, I also compute the shared secret on my side. Since I intercepted Alice's public key \( A \), I use my private key \( b_{\text{mine}} \) to compute the shared secret:
\[
ss_{\text{mine}} = A^{b_{\text{mine}}} \mod p = A^3 \mod p
\]
This gives me the same shared secret as Alice, allowing me to decrypt any encrypted messages exchanged between Alice and Bob.

---

### 6. Final Shared Secret

- Alice computes her shared secret using:
  \[
  ss_{\text{alice}} = B_{\text{mine}}^a \mod p
  \]
- I compute the shared secret using:
  \[
  ss_{\text{mine}} = A^{b_{\text{mine}}} \mod p
  \]

Since both values represent the same shared secret, I am now able to intercept and decrypt any encrypted messages, since I possess the same shared secret as Alice.
