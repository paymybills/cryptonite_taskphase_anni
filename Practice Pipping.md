## Practice Piping

---

### Redirecting Output

To solve this problem, I used input redirection to write "PWN" into a file called "COLLEGE." I ran the `echo` command with the `>` operator to redirect the output:

```bash
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
```

**Result:** Redirected 'PWN' to 'COLLEGE'! Here’s the flag:

```
pwn.college{Azwr6eJ66Z8ieuY2dt9zs2dCAJh.dRjN1QDLxcDO0czW}
```

---

### Redirecting More Output

For this challenge, I redirected the output of `/challenge/run` to a file called "myflag" and checked the file contents using `cat` to confirm it worked:

```bash
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
hacker@piping~redirecting-more-output:~$ cat myflag
```

**Flag:** 

```
pwn.college{MitsK03xQxVnMWJG65lRtgBO4YW.dVjN1QDLxcDO0czW}
```

---

### Appending Output

To save the output of `/challenge/run` without losing previous data, I switched to append mode using `>>`. This way, I captured both halves of the flag without issues:

```bash
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
```

**Output:**

```
This is the first half:
pwn.college{U7Wg_uVwogGNsasDH8KuCJzHoGG.ddDM5QDLxcDO0czW}
that is the second half
```

---

### Redirecting Errors

For this challenge, I redirected both stdout and stderr separately. I sent stdout to "myflag" and stderr to "instructions" using:

```bash
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag
```

**Flag:** 

```
pwn.college{IWZ8msGBEUDOY0B9Chme2s9fSHU.ddjN1QDLxcDO0czW}
```

---

### Redirecting Input

In this challenge, I used input redirection to feed a file into `/challenge/run`. First, I created the file `PWN` with the content "COLLEGE" and then redirected that file into the command using `<`:

```bash
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
```

**Output:**

```
Correct! You redirected the PWN file into my standard input and read 'COLLEGE'!
Here’s your flag:
pwn.college{ks2FzPsFkGn-1MXgDdntrqoy3po.dBzN1QDLxcDO0czW}
```

---

### Grepping Stored Results

For this challenge, I redirected the output from `/challenge/run` to `/tmp/data.txt` and searched for the flag using `grep`:

```bash
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
```

**Flag:**

```
pwn.college{cuwFD51UCBg_nO0HK2KSX2AEv6O.dhTM4QDLxcDO0czW}
```

---

### Grepping Live Output

For this challenge, I simplified finding the flag with the pipe operator (`|`). I piped the output of `/challenge/run` directly into `grep`:

```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
```

**Flag:**

```
pwn.college{Qhryqu3rV_5uLjtaTFJ2ZBOAmZ0.dlTM4QDLxcDO0czW}
```

---

### Grepping Errors

In this task, I needed to search through standard error output directly. I redirected stderr to stdout using `2>&1`, so both could be piped into `grep`:

```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
```

**Flag:**

```
pwn.college{MBYjCqyG00lf0byzFiq0k808PUI.dVDM5QDLxcDO0czW}
```

---

### Duplicating Piped Data with Tee

For this challenge, I used the `tee` command to view data flowing through the pipe while passing it to another command. I piped the output of `/challenge/pwn` into `/challenge/college`, saving it to `intercepted_output`:

```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret "0briYS5Q" | tee intercepted_data | /challenge/college
```

**Flag:**

```
pwn.college{0briYS5Q-mt423lKUDLNIUyP3Pn.dFjM5QDLxcDO0czW}
```

---

### Writing to Multiple Programs

In this challenge, I took the output from `/challenge/hack` and passed it to both `/challenge/the` and `/challenge/planet` using `tee` and process substitution:

```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >( /challenge/the ) >( /challenge/planet )
```

---

### Split Piping Stderr and Stdout

In this task, I redirected the output from `/challenge/hack` so that stdout went to `/challenge/planet` and stderr went to `/challenge/the`:

```bash
hacker@piping~split-piping:~$ /challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )
```

**Execution:** Both stdout and stderr were separated properly and handled as needed.

---
