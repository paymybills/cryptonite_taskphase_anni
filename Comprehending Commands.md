# Comprehending Commands

### `cat`: Not the Pet, but the Command!
To solve this challenge, the `cat` command was utilized, which is one of the most useful Linux tools for reading files. The task was to read a flag file located in the home directory. Navigating to the home directory and executing the command `cat flag` displayed the contents of the flag file directly in the terminal. This was a straightforward solution:
```bash
cd ~
cat flag
```

### Catting Absolute Paths
In this challenge, the `cat` command was again used, but this time the absolute path to the flag file had to be specified. The flag was stored in `/flag`, so the command executed was:
```bash
cat /flag
```
Additionally, a video was referred to for deeper understanding: [More Catting Practice](https://youtu.be/QFIq_e5t6iQ?si=LjseI-tjGvcaWMaV).

### Grepping for a Needle in a Haystack
For this challenge, the file contained a hundred thousand lines of text, making `cat` alone impractical. Instead, the `grep` command was employed to search for a specific pattern identifying the flag. Given that the hint indicated the flag starts with "pwn.college," the following command was executed:
```bash
grep 'pwn.college' /challenge/data.txt
```
This quickly identified the line containing the flag.

### Listing Files
To locate a file with a random name in the `/challenge` directory, the `ls` command was utilized, which lists the contents of directories. The command executed was:
```bash
ls /challenge
```
This revealed the randomly named file that needed interaction.

### Touching Files
In this challenge, the task was to create two files in the `/tmp` directory using the `touch` command. First, navigation to the `/tmp` directory was necessary, followed by executing the commands:
```bash
touch /tmp/pwn
touch /tmp/college
```
These commands created the required blank files. Afterward, the command `/challenge/run` was executed to retrieve the flag.

### Removing Files
The goal here was to delete the `delete_me` file from the home directory. Initially, the contents of the directory were listed to confirm the file's presence, and then the following command was executed:
```bash
rm ~/delete_me
```
Afterward, running `/challenge/check` confirmed that the file had been successfully deleted, and the flag was obtained.

### Hidden Files
In this challenge, the flag was concealed as a dot-prepended file, meaning it wouldn’t appear with a standard `ls` command. To solve this, the command `ls -a` was used in the root directory (`/`), which lists all files, including hidden ones. This revealed the hidden file, and after locating it, the flag was retrieved by running:
```bash
cat /flag
```
(Note: The exact command may vary.)

### An Epic File System Quest
As the task name suggests, this was indeed an epic quest. The challenge involved finding the flag hidden somewhere in the file system using the `cd`, `ls`, and `cat` commands. Starting from the root directory (`/`), the contents were listed using:
```bash
ls
```
A file labeled `HINT` was found among the various directories and files. Using:
```bash
cat HINT
```
the clue was read, leading to another location in the file system. Following the clues sequentially, navigation through directories continued until the flag was discovered. It took some time, but it was a fun process.

### Making Directories
In this task, the goal was to create a directory and a file. Navigation to the `/tmp` directory was the first step, followed by creating a new directory named `pwn` using:
```bash
mkdir /tmp/pwn
```
Then, changing into that directory and creating a file called `college` was done with:
```bash
touch /tmp/pwn/college
```
Afterward, running `/challenge/run` verified that everything was in order, allowing for the retrieval of the flag.

### Finding Files
The challenge involved locating a hidden flag in a random directory on the filesystem using the `find` command. Initially, `find` was executed without arguments to get an overview of the current directory. Then, to specifically search for the file named `flag`, the command executed was:
```bash
find / -name flag
```
Since there are multiple files with that name on the filesystem, continued searching was required until the correct one was found, demanding patience.

### Linking Files
The goal was to access the flag located in `/flag` by creating a symbolic link that redirected to a different file path. The command used was:
```bash
ln -s /flag /home/hacker/not-the-flag
```
When accessing `/challenge/catflag`, which was designed to read from `/home/hacker/not-the-flag`, it followed the symlink, providing the contents of `/flag`.
