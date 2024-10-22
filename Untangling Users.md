# Untangling Users

## Becoming Root with `su`
- Simple steps to switch to `root`:
  1. Run `su` and enter the password `hack-the-planet`.
  2. Verify by using `whoami` to confirm you're root.
  3. Run:
     ```bash
     cat /flag
     ```
  
  **Flag:**
  ```
  pwn.college{8vQkONoCT2AZNFJyk8WA9t5nOdS.dVTN0UDLxEjM2czW}
  ```

---

## Other Users with `su`

### Switching to `zardus`
1. Run:
   ```bash
   su zardus
   ```
2. Enter the password: `dont-hack-me`.
3. Execute the challenge:
   ```bash
   /challenge/run
   ```

**Flag:**
```
pwn.college{s9x062byHjzkYSEaMP7IcJvO5kF.dZTN0UDLxEjM2czW}
```

---

## Cracking Passwords with John the Ripper
1. Run John the Ripper:
   ```bash
   john /challenge/shadow-leak
   ```

2. Wait for it to finish. The cracked password is: `aardvark`.

3. Switch to `zardus`:
   ```bash
   su zardus
   ```
   Enter the password: `aardvark`.

4. Run the challenge:
   ```bash
   /challenge/run
   ```

**Flag:**
```
pwn.college{Eyz5nlGGhe66Y8jpkpocpL4RK1b.ddTN0UDLxEjM2czW}
```

---

## Using `sudo`
1. Use `sudo` to read the flag:
   ```bash
   sudo cat /flag
   ```

**Flag:**
```
pwn.college{8vAPPTFSZMB9JbutKhgAs_SJMNe.dhTN0UDLxEjM2czW}
```
