
## 10.3 Data Transfer

We can send and receive data via socket using `read()` and `write()` functions. These functions are defined as below.

```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);
```

These functions are general I/O functions. We can use specific I/O for socket operations using `send()` and `recv()` functions. They can be implemented as follows.

```c
#include <sys/types.h>
#include <sys/socket.h>

ssize_t send(int sockfd, const void *buf, size_t len, int flags);
ssize_t recv(int sockfd, void *buf, size_t len, int flags);
```

In this section we build client-server like section 10.2 but we try to transfer data using `write()` and `read()` functions.

### 10.3.1 Server

After client connected, we read data from client using `read()` function. Then we send message to client using `write()` function. After that, we close connection.

For implementation, we create a file, called `data_server.c`, and write this code.

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>
#include <errno.h>

int main(void)
{
    int sockfd, newsockfd, portno, clilen, sz;
    char buffer[256];
    struct sockaddr_in serv_addr, cli_addr;

    portno = 8059; // server port
    errno = 0;

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0)
    {
        printf("\n socket() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    bzero((char *) &serv_addr, sizeof(serv_addr));

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = INADDR_ANY;
    serv_addr.sin_port = htons(portno);

    if (bind(sockfd, (struct sockaddr *) &serv_addr,
             sizeof(serv_addr)) < 0)
    {
        printf("\n bind() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    printf("socket has created and binded\n");
    printf("listening incoming socket client...\n");

    listen(sockfd,5);
    clilen = sizeof(cli_addr);
    newsockfd = accept(sockfd, (struct sockaddr *) &cli_addr, &clilen);
    if (newsockfd < 0)
    {
        printf("\n accept() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    printf("a client was connected\n");

    // read data
    sz = read(newsockfd,buffer,255);
    if (sz < 0)
    {
        printf("\n read() failed with error [%s]\n",strerror(errno));
        return -1;
    }
    printf("Received message: %s\n",buffer);

    // write data
    sz = write(newsockfd,"this is message from server",30);
    if (sz < 0)
    {
        printf("\n write() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    // close socket
    close(newsockfd);
    close(sockfd);

    return 0;
}
```

This code is similar to code on section 10.2.1 but we continue to read and send data.

Save this code and compile it.

```bash
$ gcc -o data_server data_server.c
```

### 10.3.2 Client

On client side, we send message after connected. Then we read message from server.

Let’s start to create a file, called `data_client.c`, and write this code.

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>
#include <string.h>
#include <errno.h>

int main(void)
{
    int sockfd, portno, sz;

    struct sockaddr_in serv_addr;
    struct hostent *server;
    char buffer[256];

    // server hostname. You can change it
    char server_hostname[] = "ubuntu15";
    portno = 8059; // server port
    errno = 0;

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0)
    {
        printf("\n socket() failed with error [%s]\n", strerror(errno));
        return -1;
    }

    printf("socket has created\n");

    server = gethostbyname(server_hostname);
    if (server == NULL)
    {
        printf("\n gethostbyname() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    bzero((char *) &serv_addr, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    bcopy((char *)server->h_addr,
          (char *)&serv_addr.sin_addr.s_addr,
          server->h_length);
    serv_addr.sin_port = htons(portno);

    printf("connecting to server...\n");
    if (connect(sockfd,(struct sockaddr *)&serv_addr,sizeof(serv_addr)) < 0)
    {
        printf("\n connect() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    printf("connected to server\n");

    // write data
    strcpy(buffer,"this is message from client");
    sz = write(sockfd,buffer,strlen(buffer));
    if (sz < 0)
    {
        printf("\n write() failed with error [%s]\n",strerror(errno));
        return -1;
    }

    // read data
    bzero(buffer,256);
    sz = read(sockfd,buffer,255);
    if (sz < 0)
    {
        printf("\n read() failed with error [%s]\n",strerror(errno));
        return -1;
    }
    printf("Received message: %s\n",buffer);

    // close socket
    close(sockfd);

    return 0;
}
```

Save this code and compile it.

```bash
$ gcc -o data_client data_client.c
```

### 10.3.3 Testing

We are ready to test our client-server app. Firstly we run server app.

The following is a sample output for server app.

```text
agusk@ubuntu15:~/books/cprog$ gcc -o data_server data_server.c
agusk@ubuntu15:~/books/cprog$ ./data_server
socket has created and binded
listening incoming socket client....
a client was connected
Received message: this is message from client
agusk@ubuntu15:~/books/cprog$ 
```

Then we run client app. You can see the output, shown in Figure below.

```text
agusk@ubuntu15:~/books/cprog$ gcc -o data_client data_client.c
agusk@ubuntu15:~/books/cprog$ ./data_client
socket was created
connecting to server....
connected to server
Received message: this is message from server
agusk@ubuntu15:~/books/cprog$ 
```

## Contact and Source Code

If you have question related to this book, please contact me at aguskur@hotmail.com. My blog: [http://blog.aguskuriawan.net](http://blog.aguskuriawan.net)

You can download source code for this book on [http://www.aguskuriawan.net/book/cprog03282015.zip](http://www.aguskuriawan.net/book/cprog03282015.zip)
