# Level02
## Step by step
- In the user `level02` home directory, there is a file
  ```bash
  > ls
  level02.pcap
  ```
- The `.pcap` is an abreviation for `packet capture`, PCAP files store network data gathered by the network-traffic-capturing program tcpdump
- Download the file in my machine
  ```bash
  > scp -P 4243 level02@127.0.0.1:~/level02.pcap .
  ```
- Use Docker to download  `tshark` and `xxd`
  ```bash
  > docker run --rm -it --name SnowCrashFlag02 -v ${PWD}:/Flag02 debian bash
  > apt update; apt install tshark -y; apt install xxd -y
  ```
- With the command `tshark`, I parse data send in the communications
  ```bash
  > tshark -r /test/level02.pcap -T fields -e tcp.payload | xxd -r -p

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
  There is a password `ft_wandrNDRelL0L` but it's not the flag
  ```bash
  > tshark -r /test/level02.pcap -T fields -e ip.src -e ip.dst -e tcp.payload
  
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
  After removing every character delete, the password is `ft_waNDRelL0L`
- Flag02 is `ft_waNDRelL0L`
