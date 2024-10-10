Hello Hackers
Intro to Commands:

A very monkey see, monkey do approach. Using whoami tells me that my name is "hacker." I invoked the hello command as instructed and got the flag.
Intro to Arguments:

Another monkey see, monkey do scenario. There was a command called echo, and it accepted an argument. After entry, it processed the argument and printed out whatever the argument was.

This time, the flag was obtained by running hello hackers where hello was the command and hacker was the argument.

That concludes Module 1.
Pondering Paths

The file system is a tree. Each vertex has a path associated with it, and no two adjacent vertices (nodes of the same depth) are connected. You can traverse up and down the path.

Oh, and a path is the connection of nodes leading up to the desired vertex.
The Root:

Invoke pwn using its absolute path, which is /pwn.
Program and Absolute Paths:

I knew I had to go to run, and run was inside challenge, so the absolute path is /challenge/run.
Position Thyself:

I navigated to /challenge, used ls and saw run was in there. I tried /challenge/run but got the message:

bash

You are not currently in the /home directory. 
Please use the cd utility to change directory appropriately.

I did cd /home, traversed there, and ran /challenge/run. Found the flag.
Position Elsewhere:

I tried running /challenge/run again and saw that /proc/785/fd was the desired location for accessing it. I cd-ed there and ran /challenge/run. Found the flag.
Position Yet Elsewhere:

Same process again. I ran /challenge, saw I needed /temp as my current directory, went there, and then ran /challenge/run.
Implicit and Explicit Paths
Implicit Relative Paths, from /:

Ran /challenge/run. It didn't work, so I navigated to / with cd /, then used the hint to realize I should use:

arduino

./challenge/run

Explicit Relative Paths, from /:

Repeated the process. cd / and then ran:

arduino

./challenge/run

Implicit Path:

Went to cd home, then navigated from there to /challenge, and ran:

arduino

./run

Home Sweet Home:

This step required two constraints:

    Use an absolute path starting from /.
    Must be in the /home directory, specifically /home/hacker.

Additionally, the argument needed to be less than three characters before expansion.

So, I used ~ to represent /home/hacker (making things 1 character). Created a file ~/f with a filename, then let it rip:

bash

/challenge/run~/f

What happened was ~/f expanded to /home/hacker/f, and the program wrote the flag to the file and read it back to me.
