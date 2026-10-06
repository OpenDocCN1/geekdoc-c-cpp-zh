additional function that is called to actually crash the application. So we know that somewhere around that area should be a safe place to jump. To be sure, we can create a NOP sled, or a padding of NOP instructions which tell the application to do nothing and move on. By NOP is a computer instruction that does nothing and moves on. By adding these NOP instructions, we can create a landing pad for our code. Let's modify our code for the new information we have.

```
#!/usr/bin/python
import socket
s = socket.socket()
host = '127.0.0.1'
port = 8000
eip = "\x30\xcc\xff\xff"
buf = "\A"*268 + eip + "\x90"*32
buf += "\xCC"*(1024-len(buf))
s.connect((host, port))
print s.recv(1024)
s.send(buf)
print s.recv(1024)
s.close
```

We can see a few modifications here. We have modified the EIP value and set it to the value of a space on our stack. The x86 platform is little endian, and we have to put the location jump in reverse order. This makes 0xffffcc30 turn into 0x30ffff. Next, we update our buffer to have our additional 32 bytes of NOP instructions (0x90) Finally we change the last portion of our buffer from C's to "\xCC". This is the code for INT interrupt that will cause the debugger to stop. This will tell us that our code has successfully executed once we run it. Let's give it a go.

# Note

The term little endian is a term used by computer scientists to define the order in which hardware reads data. In big endian format (if there was a little endian, there'd be a big one, right?), For little endian, it's reversed! In our example, notice that we have not entirely reversed the string; rather, we have preserved pairs of digits, and flipped them. We change the order of the byte in the sequence pairs are bytes.