```
```bash
agusk@ubuntu15:~/books/cprog$ gcc -c -I/usr/include/mysql demo-connection.c
agusk@ubuntu15:~/books/cprog$ gcc -o demo-connection demo-connection.o -L/usr/lib/mysql -lmysqlclient
agusk@ubuntu15:~/books/cprog$ ./demo-connection
connecting to mysql server...
connected.
closing connection...
closed.
agusk@ubuntu15:~/books/cprog$ 
```
```