
## Shell Variables

### Printing Variables
The flag is stored in a variable called `FLAG`. We print a variable using `$`, by prepending `$` to the variable name.

```bash
echo $FLAG
```

Output:
```
pwn.college{IGPa6vTU2ReV1ZVn_ym95nxrAT-.ddTN1QDLxEjM2czW}
```

### Setting Variables
Just set the variable `PWN` to `College`, but no spaces, because then it would try to run `PWN`.

```bash
PWN=College
```

Output:
```
pwn.college{IGPa6vTU2ReV1ZVn_ym95nxrAT-.ddTN1QDLxEjM2czW}
```

### Multiword Variable
You have to pass it as a single token, so use quotes `""`.

```bash
PWN="COLLEGE YEAH"
```

Output:
```
pwn.college{44oHksUHrBdXmLyMgGx9oxiJ0YV.dBjN1QDLxEjM2czW}
```

### Exporting Variables
If you set a variable in one instance, it isn't a permanent change to that variable. To make sure the value is retained, you need to export the variable.

```bash
export VAR
```

In this case:
```bash
PWN=COLLEGE
export PWN
/challenge/run
```

Output:
```
pwn.college{s-JwpZPk5pkEbhDRiljnyHgEncG.dJjN1QDLxEjM2czW}
```

### Printing Exported Variables
Just list out all the environment variables and then sift through for the flag.

```bash
export -p
```

Output:
```
pwn.college{wdLu0Z-OM2jOtbFXLiB8Ej4hjku.dhTN1QDLxEjM2czW}
```

### Storing Command Output
You can store the output of a command into a variable.

```bash
PWN=$(/challenge/run)
```

Then, just echo the variable:

```bash
echo $PWN
```

Output:
```
pwn.college{4YdvD2_hIo5-tiv7QuaSStyhUbc.dVzN0UDLxEjM2czW}
```

### Reading Input
You can read user inputs and assign that value to a variable.

```bash
read -p "Enter value: " PWN
```

Got the flag:

```
pwn.college{E3By4Uli4N34c71ue3DZ3Nekx0-.dhzN1QDLxEjM2czW}
```

Additional syntax options for `read`:

```bash
read [-ers] [-a array] [-d delim] [-i text] [-n nchars] [-N nchars] [-p prompt] [-t timeout] [-u fd] [name ...]
```
