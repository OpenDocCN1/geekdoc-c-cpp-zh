```
```c
printf("%s\n",buffer);

sprintf(&msg[24], "%d",count);
count++;
sendto(sock, &msg, strlen(msg), MSG_CONFIRM,
    (struct sockaddr *)&clientaddr, len);
}
close(sock);
}
```
```

Figure 14.3 MyServer.c

There are many UDP apps available on the Play Store free of charge. In this project, the UDP Terminal by mightyIT is used (see Figure 14.4). Enter the port number and IP address of your Android smartphone and click Start Terminal as shown in Figure 14.5. An example run of the program is shown in Figure 14.6, where both the smartphone and PC screen are shown.

![](bbox=[0.3, 0.52, 0.7, 0.7])

Figure 14.4 UDP Terminal apps on Android smartphone

![](bbox=[0.42, 0.76, 0.58, 0.9])

Figure 14.5 Enter the port numbers