when the client has entered new data.

```
# otherwise, it's a command to execute
else:
command = sock.recv(1024)
if command:
    shell = command.rstrip().split(" ")
    try:
        out = subprocess.Popen(shell, stdout=subprocess.PIPE).communicate() [0]
    except:
        out = "Command failed\n"
        sock.send(out)
else:
    sock.close()
input.remove(sock)
```

If the socket wasn't the same as our listener socket, we have a client who has sent us information. We can read that information into a string called command. If no data was waiting, it means the socket has shut down and we need to close it. If data was waiting, we need to clean it up to get ready to execute it. First we strip any whitespace from the end, and then we split into individual arguments to be passed into the shell. Our network shell will only work with commands, so some things like cd (change directory) may not work. Since we know that some commands may fail, we wrap our process creation command in error handling so that we don't crash the program.

Next, we execute our command. Using Popen, for process open, we create a process using the arguments that were passed from the client, and redirect output to a pipe. The communicate function will interact with the program and return a list of output. We want the first element of that list to be sent back to the client, so we use the first element of the output of the communicate method. Next we send the output back to the client and return to our loop, waiting for more input.

We should now have a working network shell.
#!/usr/bin/python
import socket, select,os, subprocess
# Create and bind socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)