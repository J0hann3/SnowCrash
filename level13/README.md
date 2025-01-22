# Level13
## Step by step
### 1. Access the `level13` Home Directory
  ```bash
  > ls -la
  -rwsr-sr-x 1 flag13  level13 7303 Aug 30  2015 level13
  ```

---
### 2. Understanding the `level13` Program

When you run the `level13` executable, it prints:
  ```bash
  > ./level13
  UID 2013 started us but we we expect 4242
  ```
The goal is to change the UID from 2013 to 4242.

---
### 3. Debugging with GDB

Start `gdb` to debug the program:
  ```bash
  > gdb ./level13
  > start
  > ni # until thee call of getuid()
  > set $eax=0x1092
  > ni #until the call of printf to print the token
  > print(char*)$eax
  XXX
  ```
