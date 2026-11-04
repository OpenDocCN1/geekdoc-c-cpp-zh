```
```c
serveraddr.sin_family = AF_INET;
serveraddr.sin_addr.s_addr = INADDR_ANY;
serveraddr.sin_port = htons(Port);
bind(sock,(struct sockaddr *)&serveraddr, sizeof(serveraddr));
listen(sock, 5);
cli = accept(sock, NULL,NULL);

//
// Get reply from the HTTP and process it, send the html page
//

    while(1)
    {
        num = recv(cli, buffer, sizeof(buffer),0);
        buffer[num] = '\0';
        if(strstr(buffer,"LED=ON"))digitalWrite(LED, HIGH);
        if(strstr(buffer,"LED=OFF"))digitalWrite(LED, LOW);
        if(strstr(buffer,"LED1=ON"))digitalWrite(LED1, HIGH);
        if(strstr(buffer,"LED1=OFF"))digitalWrite(LED1, LOW);
        cli = accept(sock,NULL,NULL);

        send(cli,html,sizeof(html),0);
    }
}
```
```

Figure 14.21 Program WEBSERVER.c

Notice Port 80 may be used by other programs on your Raspberry Pi. As a result, your project may not work. You can find out the ports and the programs that use these ports by entering the command `sudo netstat -tlnpu` as shown in Figure 14.22 (only part of the display is shown here).

![](bbox=[0.157, 0.642, 0.782, 0.891])

Figure 14.22 Ports used on author’s Raspberry Pi