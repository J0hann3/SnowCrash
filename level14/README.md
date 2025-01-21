# Level14
## Step by step
### 1. Navigate to the `level14` Home Directory
  ```bash
  > ls -la
  ```
You’ll notice it is empty, and there is nothing related to `flag14` or other resources that belong to `level14`.

---
### 2. Reverse Engineering the getflag Binary

The only solution is to reverse engineer the getflag binary using GDB:
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
