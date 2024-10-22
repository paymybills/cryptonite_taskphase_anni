# Perceiving Permission

## Changing File Ownership
- Used `ls -l` on `/flag`  
  Saw that `root` was the owner.
  
- Command:  
  ```bash
  chown hacker /flag
  ```

- Verified with:  
  ```bash
  ls -l /flag
  ```
  Output:  
  ```
  hacker  root
  ```

- Now that I owned it, I ran:  
  ```bash
  cat /flag
  ```
  **Flag:**  
  ```
  pwn.college{cDi_rc9VoZrPYXSr5IAyykmJ_G1.dFTM2QDLxEjM2czW}
  ```

---

## Groups and Files
So basically...

---

## Fun with Group Names
- Used `id` to find out which group I am in. Found out that I'm in `11637`.

- Command:  
  ```bash
  chgrp 11637 /flag
  ```

- Verified with:  
  ```bash
  ls -l /flag
  ```
  Output:  
  ```
  root 11637
  ```

- Ran:  
  ```bash
  cat /flag
  ```
  **Flag:**  
  ```
  pwn.college{AyiwtU6s9fuVZjboZNGsVxYMB5i.dJzNyUDLxEjM2czW}
  ```

---

## Changing Permissions
- First, find who and what is allowed to access the flag:  
  ```bash
  ls -l /flag
  ```
  Output:  
  ```
  -r-------- 1 root root 58 Oct 22 18:06 /flag
  ```

- Only `root` has read access. Grant access to `hacker`:  
  ```bash
  chmod o+r /flag
  ```

- Verified with:  
  ```bash
  ls -l /flag
  ```
  Output:  
  ```
  -r-----r-- 1 root root 58 Oct 22 18:06 /flag
  ```

- Ran:  
  ```bash
  cat /flag
  ```
  **Flag:**  
  ```
  pwn.college{Yzejn2R9I0B4-HDfFQ9hcIpIH7V.dNzNyUDLxEjM2czW}
  ```

---

## Executable Files
- Goal: Make `/challenge/run` executable for `hacker`.

- First, verify permissions:  
  ```bash
  ls -l /challenge/run
  ```

- Add execute permissions:  
  ```bash
  chmod u+x /challenge/run
  ```

- Verified with:  
  ```bash
  ls -l /challenge/run
  ```
  Output:  
  ```
  -r-xr--r-- 1 hacker hacker 32 Jul 4 06:37 /challenge/run
  ```

- Ran the executable:  
  **Flag:**  
  ```
  pwn.college{gJHM2EOcgd0G0ffWgOGSKi0MpF2.dJTM2QDLxEjM2czW}
  ```

---

## Permission Tweaking Practice
- Current permissions of `/challenge/pwn`:  
  ```
  rw-r--r--
  ```

- Needed permissions:  
  ```
  ------r--
  ```

### Steps:
1. **Remove user and group execute and write permissions**:  
   ```bash
   chmod u+x,g+wx /challenge/pwn
   ```

2. **Remove all group permissions**:  
   ```bash
   chmod g-rwx /challenge/pwn
   ```

3. **Remove user execute permissions**:  
   ```bash
   chmod u-x /challenge/pwn
   ```

4. **Set permissions for user, group, and world**:  
   ```bash
   chmod u=wx,g=wx,o=r /challenge/pwn
   ```

5. **Remove all permissions**:  
   ```bash
   chmod a-rwx /challenge/pwn
   ```

6. **Add write permissions to the user**:  
   ```bash
   chmod u+w /challenge/pwn
   ```

7. **Add read permissions for user and world**:  
   ```bash
   chmod u+r,o+rw /challenge/pwn
   ```

### Flag File:
- To make the `/flag` file readable for the user:  
  ```bash
  chmod u+r /flag
  ```

**Flag:**  
```
pwn.college{w3WOkogjSDJToB-DUtxJ4yXXyoy.dBTM2QDLxEjM2czW}
```

---

## SUID Bit
- Check the permissions:  
  ```bash
  ls -l /challenge/getroot
  ```

- Set the SUID bit:  
  ```bash
  chmod u+s /challenge/getroot
  ```

- Execute the program:  
  ```bash
  /challenge/getroot
  ```

- Found files using `ls`. The flag was in `not-the-flag`:  
  ```bash
  cat not-the-flag
  ```

**Flag:**  
```
pwn.college{oRdJKWViyunWAbwErnr4cO9tRnf.dNTM2QDL4czN0czW}
```
