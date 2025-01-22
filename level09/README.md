# Level09
## Step by step
### 1. Access the user `level09` home directory
  ```bash
  > ls -la
  -rwsr-sr-x 1 flag09  level09 7640 Mar  5  2016 level09
  ----r--r-- 1 flag09  level09   26 Mar  5  2016 token
  ```
---

### 2. Understanding the Executable

  - The `level09` executable takes an argument and performs some modifications to it.
  - The `token` file contains the following content:`f4kmm6p|=�p�n��DB�Du{��`
---
### 3. Decrypting the Token
Lets reverse the encrypting `token`

  ```bash
  > scp -P 4243 ./main.c level09@127.0.0.1:/tmp/main.c
  
  > cd /tmp
  > gcc main.c
  > ./a.out $(cat ~/token)
  XXX
  ```
