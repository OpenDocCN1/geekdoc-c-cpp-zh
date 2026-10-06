name or IP address and the port that we wish to connect. connect statement opens the connection to the remote host. Now we have the ability to read and write to that socket. Let’s look at some basic code to fetch a Web page from the remote host.

```
# send a basic http request
s.send("GET / HTTP/1.0\nHost: www.google.com\n\n")
page = ""
# while data is still coming back, append to our page variable
while 1:
data = s.recv(1024)
if data == "":
    break
page = page + data
```

The socket method takes a single argument: the string that you wish to send. Here, we are sending a Web request to Google. We initialize our page variable to an empty string. Finally, we create and use a loop to receive data. We want a loop because recv will read up to the amount of data specified as an argument—in this case 1024 bytes. We want to keep reading until we have all the data. recv method will return an empty string when there is no more data to read, so we check for that condition to break out of our while loop. Once we have data, we close our socket and print the data. Let’s look at our finished script:

```
#!/usr/bin/python
import socket
# Build a socket and connect to google.com
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("www.google.com",80))
# send a basic http request
s.send("GET / HTTP/1.0\nHost: www.google.com\n\n")
page = ""
# while data is still coming back, append to our page variable
while 1:
data = s.recv(1024)
if data == "":
    break
page = page + data
# close our socket and print the results
s.close()
print page
```

This script will handle IPv4 sockets. But what if we want to use