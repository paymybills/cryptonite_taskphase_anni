## Matching with *

To tackle this challenge, I utilized shell globbing for efficient directory navigation. Starting from my home directory, I employed the wildcard character `*` to match the path. Given that I needed to limit the argument to four characters, I used the command:
```bash
cd /ch*
```
This allowed the shell to recognize and complete the path to `/challenge`. Once inside the challenge directory, I executed the `/challenge/run` command, successfully capturing the flag.

```
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{A4R9dzpA-RMFYOmrVbJIo6yiA1Y.dFjM4QDLxcDO0czW}
```

---

## Matching with ?

In this part, I employed the `?` wildcard to replace specific letters in the directory name. Starting from my home directory, I typed:
```bash
cd /?ha??enge
```
Here, the `?` symbol represented the characters `c` and `l` in "challenge." This allowed the shell to match the correct directory without needing to type the full name. After navigating to `/challenge`, I ran the `/challenge/run` command to retrieve the flag.

```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{EOCQEincxnGKAaxCyXLDur23xxe.dJjM4QDLxcDO0czW}
```

---

## Matching with []

To begin, I navigated to the `/challenge/files` directory using:
```bash
cd /challenge/files
```
Once there, I executed the command:
```bash
/challenge/run file_[absh]
```
The square brackets enabled me to target specific files: `file_b`, `file_a`, `file_s`, and `file_h`. By matching any of the listed characters in that position, the shell correctly identified the files. After running the command, I was able to capture the flag.

```
hacker@globbing~matching-with-:/challenge$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[abhs]
You got it! Here is your flag!
pwn.college{klN21LvRxJSUajYbUrUtszznEzz.dNjM4QDLxcDO0czW}
```

---

## Matching Paths with []

To solve this, I employed bracket globbing to target specific files by their absolute paths. Starting from my home directory, I executed:
```bash
/challenge/run /challenge/files/file_[absh]
```
In this case, the square brackets allowed me to match the characters for the specific files: `file_b`, `file_a`, `file_s`, and `file_h` within the `/challenge/files` directory.

```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{U_9dK4YFZ815DFXVVfGkuv4Wywn.dRjM4QDLxcDO0czW}
```

---

## Exclusionary Globbing

To tackle this challenge, I used the bracket inversion technique to filter out files that begin with specific characters. First, I navigated to the `/challenge/files` directory:
```bash
cd /challenge/files
```
Once there, I ran the command:
```bash
/challenge/run [!pwn]*
```
In this command, the `!` inside the brackets excluded any files starting with `p`, `w`, or `n`. The `*` wildcard ensured that all other files not beginning with those letters would be matched.

```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{wjr2jWDJi3jfmBIOg7c21SqR0tY.dZjM4QDLxcDO0czW}
```
