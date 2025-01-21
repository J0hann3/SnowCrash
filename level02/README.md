# Level02
## Step by step
### 1. Locate the file in the `level02` home directory
  ```bash
  > ls
  level02.pcap
  ```
The file `level02.pcap` is present. This is a **Packet Capture** file, which stores network data captured by tools like `tcpdump`.

---

### 2. Download the file to your local machine
Use `scp` to securely copy the `level02.pcap` file to your local machine. Adjust the IP address and port as necessary:

  ```bash
  > scp -P 4243 level02@127.0.0.1:~/level02.pcap .
  ```

---

### 3. Set up a Docker container for analysis
To analyze the `.pcap` file, you need tools like `tshark` and `xxd`. Set up a Docker container with these utilities:

  ```bash
  > docker run --rm -it --name SnowCrashFlag02 -v ${PWD}:/Flag02 debian bash
  > apt update; apt install tshark -y; apt install xxd -y
  ```

---

### 4. Analyze the `.pcap` file using `tshark`
First, parse the network data in the file:
  ```bash
  > tshark -r /Flag02/level02.pcap -T fields -e tcp.payload | xxd -r -p

  ��%��%��&���� ��#��'��$��&���� ��#��'��$�� ����#����'�������� 38400,38400����#SodaCan:0����'DISPLAYSodaCan:0����xterm��������"������!������"��"bb   B�

  �����������1������!��"����"����!��������"������"��"���	��
  �
   �����������
  Linux 2.6.38-8-generic-pae (::ffff:10.1.1.2) (pts/10)
  
  wwwbugs login: lleevveellXX
  Password: ft_wandrNDRelL0L
  
  Login incorrect
  wwwbugs login: 
  ```
This reveals a password-like string, `ft_wandrNDRelL0L`, but it is not the flag.

Next, analyze the source and destination IPs and payloads:

  ```bash
  > tshark -r /Flag02/level02.pcap -T fields -e ip.src -e ip.dst -e tcp.payload
  
  59.233.235.223	59.233.235.218	000d0a50617373776f72643a20  # mean password in ASCII
  59.233.235.218	59.233.235.223	
  59.233.235.218	59.233.235.223	66  #f
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	74  #t
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	5f  #_
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	77  #w
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	61  #a
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	6e  #n
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	64  #d
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	72  #r
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	7f  #DEL
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	7f  #DEL
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	7f  #DEL
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	4e  #N
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	44  #D
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	52  #R
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	65  #e
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	6c  #l
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	7f  #DEL
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	4c  #L
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	30  #0
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	4c  #L
  59.233.235.223	59.233.235.218	
  59.233.235.218	59.233.235.223	0d
  59.233.235.223	59.233.235.218	
  59.233.235.223	59.233.235.218	000d0a
  59.233.235.218	59.233.235.223	
  59.233.235.223	59.233.235.218	01
  59.233.235.218	59.233.235.223	
  59.233.235.223	59.233.235.218	000d0a4c6f67696e20696e636f72726563740d0a77777762756773206c6f67696e3a20
  ```
The hexadecimal payload can be converted to ASCII to reveal the password. After removing delete characters (`7f`), the reconstructed password is:

```
ft_waNDRelL0L
```

