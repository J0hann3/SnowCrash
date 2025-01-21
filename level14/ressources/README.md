# Level14
## Step by step
- The user `level14` home directory is empty, and there is nothing on the VM that it's own by him or flag14
  ```bash
  > ls -la
  ```
- The ony solution is to reverse engineering the binary `getflag` with GDB
  ```bash
  > id flag14
  uid=3014(flag14) gid=3014(flag14) groups=3014(flag14),1001(flag)

  > gdb /bin/getflag
  > b ptrace
  > b getuid
  > run
  > set $eax=0 # after the call a ptrace
  > cont
  > set $eax=3014 #after the call of getuid
  > cont
  XXX
  ```
