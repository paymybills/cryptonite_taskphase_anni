## Listing Processes:

To list all processes, use one of the following:

- `ps -ef` will show every process in full format.
- `ps aux` will list all processes along with their status and resource usage.

Ran `ps -ef`, found the challenge process, and executed it:

```bash
/challenge/16176-run-2640
```

Flag obtained:

```
pwn.college{QWtgq7wsNvkpIc3zP2xz_q51YnQ.dhzM4QDLxEjM2czW}
```

---

## Killing a Process:

1. Use `ps -ef` to find the process and its PID.
2. Execute the kill command with the PID.

In my case, the process ID was 73, so I used:

```bash
kill 73
```

Operation terminated. Ran `/challenge/run` again and got the flag.

---

## Interrupting a Process:

Use `Ctrl+C` to interrupt a running program. It’s as simple as that.

```
pwn.college{k9SuBPh_OwEb25xaTa5FQa9i3YG.dNDN4QDLxEjM2czW}
```

---

## Suspending a Process:

To suspend (pause) a process:

1. Run `/challenge/run`.
2. Suspend it using `Ctrl+Z`.
3. Now you can run another instance while the first one is suspended.

```
pwn.college{k9SuBPh_OwEb25xaTa5FQa9i3YG.dNDN4QDLxEjM2czW}
```

---

## Resuming a Suspended Process:

After suspending a process with `Ctrl+Z`, you can resume it using the `fg` command:

```bash
fg
```

Flag obtained:

```
pwn.college{AP1VLHX1tVXNt8cIOVfqseIOpKG.dZDN4QDLxEjM2czW}
```

---

## Background Processes:

1. Launch the process.
2. Suspend it (`Ctrl+Z`).
3. Background it using `bg`.
4. Launch another copy while the first one runs in the background.

```bash
/challenge/run
Ctrl+Z
bg
```

Flag obtained:

```
pwn.college{8a5OzH8PhDDuglE9r7Zq52cLiPU.ddDN4QDLxEjM2czW}
```

---

## Foreground Processes:

Move a background process back to the foreground:

```bash
/challenge/run -> Ctrl+Z -> bg -> fg -> hit Enter
```

---

## Starting a Backgrounded Process:

To start a process in the background, simply add `&` at the end:

```bash
/challenge/run &
```

Flag obtained:

```
pwn.college{A5mLhMgafYcL1ZI9zHHQyZZtu5w.dlDN4QDLxEjM2czW}
```

---

## Process Exit Codes:

You can check the exit code of the last process using `$?`. First, run:

```bash
/challenge/get-code
```

Then check or submit with:

```bash
/challenge/submit-code $?
```
