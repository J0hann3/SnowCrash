# Level13
## Step by step
- In the user `level13` home directory, there is a file
  ```bash
  > ls
  -rwsr-sr-x 1 flag13  level13 7303 Aug 30  2015 level13
  ```
-  The executable print the following when running
  ```bash
  > ./level13
  UID 2013 started us but we we expect 4242
  ```
- Lets change our UID to 4242, using GDB
  ```bash
  > gdb ./level13
  > start
  > ni # until thee call of getuid()
  > set $eax=0x1092
  > ni #until the call of printf to print the token
  > print(char*)$eax
  XXX
  ```
