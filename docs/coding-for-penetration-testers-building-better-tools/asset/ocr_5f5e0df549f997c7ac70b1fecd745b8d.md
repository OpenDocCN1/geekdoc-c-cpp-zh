```
http://local...0/etc/passwd 
localhost/systest.php?file=:cat /etc/passwd
Most Visited Offensive Security Kali Linux Kali Docs Kali Tools Exploit-DB
```

:.
b64.php
download.php
error.txt
formtest.php
get.php
index.html
logview.php
printpre.php
readwrite.php
systest.php
test.inc
variables.php
root:x:0:0:/root:/bin/bash
daemon:x:1:1:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:/bin:/usr/nologin
sync:x:3:3:/var/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin/nc

# FIGURE 5.9 Abusing the systest.php script to execute arbitrary commands.

The system command works similarly to passthru, in that it will print the output to the screen. The primary difference is that it also returns some data to us. The system function returns the last line from the output, so if we need to know what the last line is, we can perform additional operations on it. While this is sometimes useful, it is more likely that if we want to process the output from a command, we will use the exec function. The exec function takes two arguments, the command to run and a variable in which to store the results. The results will be put into the result variable as an array. By default, nothing from an exec function is printed to the screen. Let's look at an example using both types.

```
<php
print "<PRE>";nexec("ls -1",$out);
print_r($out);
print "---------------------------------\n";n$last = system("ls -1");
print "</PRE>";n?>
```