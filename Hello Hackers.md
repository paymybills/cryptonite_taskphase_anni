
---

## Intro to Commands
This module followed a straightforward approach, akin to "monkey see, monkey do." By using the command `whoami`, I discovered that my username is **hacker**. I then invoked the `hello` command as instructed, successfully capturing the flag.

## Intro to Arguments
Continuing with the same "monkey see, monkey do" method, I learned about the `echo` command, which accepts an argument. After entering the argument, the command processes it and prints out whatever was entered. This time, the flag was obtained by executing `hello hackers`, where **hello** was the command and **hacker** was the argument.

This completes Module 1.

---

## Pondering Paths

### The File System
The file system resembles a tree structure, where each vertex (or node) has a path associated with it. No two adjacent vertices (nodes at the same depth) are connected, allowing traversal up and down the path. A path is defined as the connection of nodes leading to a desired vertex.

### The Root
To invoke the program, I used its absolute path: `/pwn`.

### Program and Absolute Paths
I needed to run the program located inside the challenge directory, so I navigated to it with the path `/challenge/run`.

### Position Thyself
After changing to the `/challenge` directory using `cd /challenge` and listing the contents with `ls`, I saw that the `run` command was there. When I tried to execute `/challenge/run`, I received the following message:
```
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
```
To resolve this, I used `cd /home` to traverse to the home directory, then ran `/challenge/run` from there to successfully find the flag.

### Position Elsewhere
I attempted to run `/challenge/run` from a different location and discovered that `/proc/785/fd` was the desired location. I changed directories to `/proc/785/fd`, ran `/challenge/run`, and found the flag.

### Position Yet Elsewhere
Repeating the process, I found that to run `/challenge`, I needed to navigate to `/temp`. After changing to that directory, I executed `/challenge/run` and successfully retrieved the flag.

### Implicit Relative Paths
Starting from the root (`/`), I ran `/challenge/run`, which didn’t work. I then navigated to the root with `cd /`, and used the hint to realize I should run `./challenge/run`.

### Explicit Relative Path from Root
Following the same logic, I executed `cd /`, and then ran `./challenge/run`.

### Implicit Path
I changed to the home directory with `cd home`, then moved on to `/challenge` and executed `./run`.

### Home Sweet Home
To satisfy the constraints of the challenge, I needed to consider:
1. The absolute path should start with `/`.
2. I must be in the home directory, specifically `/home/hacker`.
3. The argument must be less than three characters **before** expansion.

To achieve this, I used `~` to represent `/home/hacker`, reducing the character count. I created a file with the name `f` in the home directory (`~/f`), then executed the command:
```bash
/challenge/run ~/f
```
In this case, `~/f` expanded to `/home/hacker/f`, and the program wrote the flag to the file and then read it back to me.

