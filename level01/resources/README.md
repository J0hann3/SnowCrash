# Level01
## Step by step
- Search in every regular files if it contains the word `flag01`
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
- In the file `/etc/passwd` there is the hash of the password
```
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```
- Download the file `/etc/passwd` on my machine with `SCP`
```bash
> scp -P 4243 level01@127.0.0.1:/etc/passwd .
```
- Using `John the Ripper` to decrypt the password
```bash
> docker run --rm -it --name SnowCrashFlag01 -v ${PWD}:/Password debian bash
> apt update; apt install john -y
> john /Password/passwd --show

flag01:abcdefg:3001:3001::/home/flag/flag01:/bin/bash

1 password hash cracked, 0 left
```
- Flag01 is `abcdefg`
