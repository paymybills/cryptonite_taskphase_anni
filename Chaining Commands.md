## Chaining Commands

### Chaining with Semicolons

You can execute multiple commands in sequence by chaining them with semicolons (`;`):

```bash
/challenge/pwn; /challenge/college
```

This runs both commands in the order they are written. The flag from this chaining sequence is:

```bash
Flag: pwn.college{Y173WxVA6NcukuYmjWLIEL__5T8.dVTN4QDLxEjM2czW}
```

---

## Shell Scripting

### Creating a Shell Script

You can put multiple commands into a script and execute them all at once. First, open a text editor such as `nano` and create a new file called `x.sh`:

```bash
nano x.sh
```

In the file, input the following:

```bash
/challenge/pwn
/challenge/college
```

After writing the commands, save and exit by pressing `CTRL + X`, then `Y`, and finally `Enter`. To execute the script, use:

```bash
bash x.sh
```

The flag obtained from this script execution is:

```bash
Flag: pwn.college{Y_D4bEs8_kBKiMKOJg76y65uGzc.dFzN4QDLxEjM2czW}
```

---

## Redirecting Script Output

This time, we’ll redirect the output of the script to another command using a pipe (`|`).

Start by creating the same shell script:

```bash
nano x.sh
```

Inside the file, write:

```bash
/challenge/pwn
/challenge/college
```

But this time, instead of simply running the script, we’ll pipe its output into `/challenge/solve`:

```bash
bash x.sh | /challenge/solve
```

This command runs the script and redirects the output into another program. The flag from this operation is:

```bash
Flag: pwn.college{8niSiXszAQS_JxjZwyucYIxnosN.dhTM5QDLxEjM2czW}
```

---

## Executing Shell Scripts

Now, let's make the shell script executable on its own:

1. Start by creating the script:

```bash
nano solve.sh
```

Inside the file, add your commands (for example, `/challenge/pwn` and `/challenge/college`):

```bash
/challenge/pwn
/challenge/college
```

2. Make the script executable using the `chmod` command:

```bash
chmod +x solve.sh
```

3. Now run the script directly:

```bash
./solve.sh
```

Once executed, you will receive a flag as follows:

```bash
Flag: pwn.college{QY9uOxCeucPCplQWHVaWRwd0wbX.dRzNyUDLxEjM2czW}
```

---
