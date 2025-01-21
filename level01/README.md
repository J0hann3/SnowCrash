# Level01
## Step by step
### 1. Search for files containing `flag01`
Use the `find` command to search for all regular files containing the word `flag01`. Suppress errors by redirecting them to `/dev/null`:
```bash
> find / -type f -exec grep -H "flag01" {} + 2>/dev/null

/etc/group:flag:x:1001:flag00,flag01,flag02,flag03,flag04,flag05,flag06,flag07,flag08,flag09,flag10,flag11,flag12,flag13,flag14
/etc/group:flag01:x:3001:
/etc/passwd:flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
Binary file /proc/2147/task/2147/cmdline matches
Binary file /proc/2147/cmdline matches
/rofs/etc/group:flag:x:1001:flag00,flag01,flag02,flag03,flag04,flag05,flag06,flag07,flag08,flag09,flag10,flag11,flag12,flag13,flag14
/rofs/etc/group:flag01:x:3001:
/rofs/etc/passwd:flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```
The file `/etc/passwd` contains a hash for `flag01`.

---

### 2. Extract the hash from `/etc/passwd`
The relevant line from `/etc/passwd` is:
```
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```
The hash is `42hDRfypTqqnw`.

---

### 3. Download the file to your local machine
Use `scp` to securely copy the `/etc/passwd` file to your local machine. Replace `level01@127.0.0.1` with your actual username and IP if necessary:

```bash
> scp -P 4243 level01@127.0.0.1:/etc/passwd .
```

---

### 4. Crack the hash using `John the Ripper`
Run a Docker container with a Debian image to install and use `John the Ripper`:

```bash
> docker run --rm -it --name SnowCrashFlag01 -v ${PWD}:/Password debian bash
> apt update; apt install john -y
> john /Password/passwd --show

flag01:abcdefg:3001:3001::/home/flag/flag01:/bin/bash

1 password hash cracked, 0 left
```
---

### 5. Conclusion
The flag for `flag01` is:
