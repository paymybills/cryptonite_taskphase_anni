# File Globbing

### Matching with `*`

#### Using Shell Globbing
To solve this challenge, shell globbing was utilized to change directories efficiently. Starting from the home directory, the wildcard character `*` was employed to match the path. Since the argument needed to be limited to four characters, the command `cd /ch*` was executed, allowing the shell to recognize and complete the path to `/challenge`. Once inside the challenge directory, the command `/challenge/run` was executed to successfully capture the flag.



### Matching with `?`

#### Replacing Specific Letters
In this challenge, the `?` wildcard was used to replace specific letters in the directory name. Starting from the home directory, the command `cd /?ha??enge` was executed, where the `?` symbol stood in for the `c` and `l` in "challenge." This allowed the shell to match the correct directory without typing the full name. After navigating to `/challenge`, the command `/challenge/run` was run to grab the flag.

### Matching with `[]`

#### Targeting Specific Files
First, navigation to the `/challenge/files` directory was performed using `cd /challenge/files`. Once there, the command `/challenge/run file_[absh]` was executed. The square brackets allowed targeting specific files: `file_b`, `file_a`, `file_s`, and `file_h`. The brackets matched any of the listed characters in that position, allowing the shell to pick only those files. After running the command, the flag was successfully captured.



### Matching Paths with `[]`

#### Using Bracket Globbing for Absolute Paths
To solve this, bracket globbing was utilized to target specific files by their absolute paths. Starting from the home directory, the command `/challenge/run /challenge/files/file_[absh]` was executed. Here, the square brackets matched the characters for the specific files `file_b`, `file_a`, `file_s`, and `file_h` in the `/challenge/files` directory.



### Exclusionary Globbing

#### Filtering Out Specific Characters
To solve this, the bracket inversion technique was used to filter out files that start with specific characters. First, navigation to the `/challenge/files` directory was completed with `cd /challenge/files`. Once there, the command `/challenge/run [!pwn]*` was executed, which used the `!` inside the brackets to exclude any files starting with `p`, `w`, or `n`. The `*` wildcard ensured that any other files not beginning with those letters would be matched.
BIOg7c21SqR0tY.dZjM4QDLxcDO0czW}

