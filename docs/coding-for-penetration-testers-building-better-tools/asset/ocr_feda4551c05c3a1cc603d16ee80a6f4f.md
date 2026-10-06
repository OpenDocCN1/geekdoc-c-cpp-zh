```
s.bind(", 8080)
# Listen for up to 10 connections
s.listen(10)
input = [s]
while 1:
    # Check for sockets waiting read
    reader,output,exceptions = select.select(input,[],[])
    for sock in reader:
        # If the socket is our listener, accept a new connection
        if sock == s:
            c,addr = s.accept()
            print("New connection from", addr)
            input.append(c)
        # otherwise, it's a command to execute
        else:
            command = sock.recv(1024)
            if command:
                shell = command.rstrip().split(" ")
                try:
                    out = subprocess.Popen(shell,stdout=subprocess.PIPE).communicate([0])
                except:
                    out = "Command failed\n"
                    sock.send(out)
                else:
                    sock.close()
                    input.remove(sock)
sock.close()
```

# Scapy

The Scapy module provides advanced packet manipulation inside the Python framework. It will allow us to manipulate and process packets at every layer of the Open Systems Interconnection stack. Scapy does sound awesome. But there is a learning curve. First we are going to look at the Scapy interactive shell to help make it familiar when we are writing script with Scapy. We will build packets to figure out how to navigate the Scapy shell, and then we will work on scripts to handle two penetration testing problems: transferring data over Internet Control Message Protocol (ICMP) and processing sniffed data.