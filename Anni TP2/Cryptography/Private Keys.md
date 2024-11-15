# Private Keys

To calculate the private key \( d \), we need to compute the modular multiplicative inverse of \( e \) modulo \( \phi(N) \), where:

- \( p = 857504083339712752489993810777 \)
- \( q = 1029224947942998075080348647219 \)
- \( e = 65537 \)
- \( \phi(N) = (p - 1) \times (q - 1) \)

Once we have \( \phi(N) \), we can calculate \( d \) using the formula:

\[
d = e^{-1} \mod \phi(N)
\]

This can be done using the Extended Euclidean Algorithm or Python's built-in function `pow(e, -1, \phi(N))` to find the modular inverse. You can try this out using the formula.

```python
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
e = 65537
phi_N = (p - 1) * (q - 1)
d = pow(e, -1, phi_N)
print(d)
```

Result:

```
121832886702415731577073962957377780195510499965398469843281
```

In syllabus for course on Elementary Number Theory, lmao.

---
