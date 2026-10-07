652 SUN's Network File System (NFS)

# 49.4 Key To Fast Crash Recovery: Statelessness

This simple goal is realized in NFSv2 by designing what we refer to as a stateless protocol. The server, by design, does not keep track of anything what is happening at each client. For example, the server does not know which clients are caching blocks, or which files are currently open at each client, or the current file pointer position for a file, etc. Simply the server does not track anything what clients are doing; rather, the protocol is designed to deliver in each protocol request all the information that is needed in order to complete the request. If it doesn't know, this stateless approach will make more sense as we discuss the protocol in detail below.

For an example of a state (not stateless) protocol, consider the open() system call. With a pathname, open() returns a file descriptor (integer) which is used on subsequent read() or write() requests to access various file blocks, as in this application code omitted for space reasons): error checking of the system call

```
char buffer[MAX];
int fd = open("", O_RDONLY); // get descriptor "fd"
read(fd, buffer, MAX); // read from foo via "fd"
read(fd, buffer, MAX); // read MAX again
...
read(fd, buffer, MAX); // read MAX again
close(fd); // close file
```

Figure 49.3: Code Reading From A File

Now that the client-side file opens the file by sending a message to the server saying "open the 'foo' and get back a 'descriptor". On subsequent reads, the server opens the file locally on its side and sends the descriptor back to the client. The client application uses that descriptor to call the read() system call; the client-side file then passes the descriptor from files in a message to the server, saying "read some bytes from the file that is referred to by the descriptor I am passing you here"

In this example, the file descriptor is a piece of shared state between the client and the server (Outsource calls this distributed state [0911]). Shared state, as we hinted complicates crash recovery. Imagine the server crashes after the first read, but before the client has issued the second. After the server is up and running again, the client issues the second read. Unfortunately, the server has no idea to which file fd is referring; that information was ephemeral (i.e., in memory) and lost when the server crashed. To handle this situation, the client and server would have to engage in some kind of recovery protocol, where the client would make sure to keep enough information around in its memory to tell the server what it needs to know (in this case, file descriptor refers to file foo).

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG