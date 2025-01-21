# Level 00
## Step by step
- Find all the files on the Vm that are owned by `flag00`
```bash
> find / -user flag00 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
```
- We get two paths to a file named `john`
```bash
> ls -la /usr/sbin/john; ls -ls /rofs/usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /rofs/usr/sbin/john
```
- In this file there is `cdiiddwpgswtgt`
```bash
> cat /usr/sbin/john
cdiiddwpgswtgt
```
- With `https://www.dcode.fr/identification-chiffrement` the cipher the most probably use is Affine Cipher
- With `https://www.dcode.fr/chiffre-affine` I decrypt the sentence and find `nottoohardhere`
- Flag00 is `nottoohardhere`
