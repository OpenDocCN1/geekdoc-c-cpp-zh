```
#include <unistd.h>

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
int listen(int sockfd, int backlog);
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
int close(int fd);
```

We usually struct sockaddr_in to pass parameter addr. It is defined as follows.

```
struct sockaddr_in {
    sa_family_t    sin_family;  /* address family: AF_INET */
    in_port_t      sin_port;    /* port in network byte order */
    struct in_addr sin_addr;    /* internet address */
};

struct in_addr {
    uint32_t       s_addr;      /* address in network byte order */
};
```

For implementation, we build server app by creating a file, called simple_server.c, and write this code.

```
1 #include <stdio.h>
2 #include <sys/types.h>
3 #include <sys/socket.h>
4 #include <netinet/in.h>
5 #include <string.h>
6 #include <errno.h>
7
8 int main(void)
9 {
10
11
12     int sockfd, newsockfd, portno, clilen;
13     struct sockaddr_in serv_addr, cli_addr;
14
15     portno = 8056; // server port
16     errno = 0;
17
18     sockfd = socket(AF_INET, SOCK_STREAM, 0);
19     if (sockfd < 0)
20     {
21         printf("\n socket() failed with error [%s]\n",strerror(errno)
22         return -1;
23     }
24
25     bzero((char *) &serv_addr, sizeof(serv_addr));
26
27     serv_addr.sin_family = AF_INET;
28     serv_addr.sin_addr.s_addr = INADDR_ANY;
29     serv_addr.sin_port = htons(portno);
```