# Level 00
## Step by step
### 1. Find all the files on the VM owned by `flag00`
```bash
> find / -user flag00 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
```
We find two paths pointing to a file named `john`.

---

### 2. Inspect the files
Check the details and permissions of both files using `ls`:
```bash
> ls -la /usr/sbin/john; ls -ls /rofs/usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /rofs/usr/sbin/john
```
Both files are identical and owned by `flag00`, with read-only permissions for everyone.

---

### 3. Read the content of the file
Use the `cat` command to view the contents of `/usr/sbin/john`:
```bash
> cat /usr/sbin/john
cdiiddwpgswtgt
```
The file contains the string `cdiiddwpgswtgt`.

---

### 4. Analyze the string
Visit [dCode](https://www.dcode.fr/identification-chiffrement) to identify the type of cipher used. The most probable cipher for this string is the **Affine Cipher**.

---

### 5. Decrypt the string
Using [dCode's Affine Cipher decoder](https://www.dcode.fr/chiffre-affine), decrypt the string `cdiiddwpgswtgt`.

Decrypted result:

```
nottoohardhere
```
