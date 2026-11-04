

```c
wiringPiI2CWrite(handle, PointerReg);
buf[0] = wiringPiI2CRead(handle);
buf[1] = wiringPiI2CRead(handle);
Temp = (buf[0] << 4) | (buf[1] >> 4);

if(Temp > 0x7FF)
{
    Temp = (~Temp) & 0xFFF;
    Temp++;
    temperature = -Temp * LSB;
}
else
    temperature = Temp * LSB;

return(temperature);
}

//
// Start of MAIN program. Read the temperature and send to Android
// smartphone when request character T is received
//
int main(void)
{
    int sock, len, num, temperature;
    char buffer[BUFFSIZE];
    struct sockaddr_in serveraddr, clientaddr;
    char msg[17] = "Temperature =  ";
    char error[] = "Error - expected T or x";
    char endofprog[] = "End of program";

    wiringPiSetupGpio();
    handle = wiringPiI2CSetup(DeviceAddress);

    sock = socket(AF_INET, SOCK_DGRAM, 0);
    len = sizeof(clientaddr);

    serveraddr.sin_family = AF_INET;
    serveraddr.sin_addr.s_addr = INADDR_ANY;
    serveraddr.sin_port = htons(Port);
    bind(sock,(struct sockaddr *)&serveraddr, sizeof(serveraddr));

    while(1)
    {
        num = recvfrom(sock, buffer, BUFFSIZE,MSG_WAITALL,
                     (struct sockaddr *)&clientaddr, &len);
        if(buffer[0] == 'x')break;
```

## 14.6 ◆ 项目 3 – 使用 UDP 与 Android 智能手机通信（树莓派作为客户端）

### 描述：
本项目使用 UDP 通信来接收数据并向 Android 智能手机发送数据。树莓派是客户端，Android 智能手机是服务器。

### 目标：
本项目旨在展示如何在树莓派与 Android 智能手机之间建立 UDP 通信。

### 框图：
框图与图 14.7 相同，但树莓派是客户端，Android 智能手机是服务器。

### 程序清单：
程序清单如图 14.10 所示（程序：MyClient.c）。

```c
/*----------------------------------------------------------------
    RASPBERRY PI - ANDROID SMARTPHONE COMMUNICATION
    ====================================================

This is UDP program. The program receives and then sends messages to
 a smartphone over the UDP socket. Program terminates when character x
 is sent from the smartphone

This is the UDP client program, communicating over port 5000

Author: Dogan Ibrahim
File  : MyClient.c
Date  : December 2020
-------------------------------------------------------------------*/

#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#define Port 5000
#define BUFFSIZE 1024

//
// Start of MAIN program
//
int main(void)
{
        int sock, len, num;
        char buffer[BUFFSIZE];
        struct sockaddr_in serveraddr;
        char msg[] = "Hello from Raspberry Pi";

        sock = socket(AF_INET, SOCK_DGRAM, 0);

        serveraddr.sin_family = AF_INET;
        serveraddr.sin_addr.s_addr = INADDR_ANY;
        serveraddr.sin_port = htons(Port);

        while(1)
        {
                sendto(sock, &msg, strlen(msg), MSG_CONFIRM,
                       (struct sockaddr *)&serveraddr, sizeof(serveraddr));

                num = recvfrom(sock, buffer, BUFFSIZE, MSG_WAITALL,
                       (struct sockaddr *)&serveraddr, &len);
                if(buffer[0] == 'x')break;
                buffer[num] = '\0';
                printf("%s\n", buffer);
        }
        close(sock);
}
```

图 14.10 程序 MyClient.c

## 14.7.4 项目 4 – 将带时间戳的温度读数发送到 Android 智能手机（树莓派作为服务器）

### 描述：
本项目将 TMP102 温度传感器芯片（见第 14.5 节）连接到树莓派。环境温度读数每 5 秒连同日期和时间连续发送到 Android 智能手机。

### 目标：
本项目旨在展示如何使用 UDP 协议通过 Wi-Fi 链路将带时间戳的温度读数发送到 Android 智能手机。

### 框图：
本项目的框图如图 14.7 所示。

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <arpa/inet.h>
#define Port 5000

int handle;

// This function reads the temperature from TMP102 and returns to
// the calling main program as a floating point number
//
float ReadTemperature()
{
    int Temp, buf[2];
    float temperature, LSB = 0.0625;

    wiringPiI2CWrite(handle, PointerReg);
    buf[0] = wiringPiI2CRead(handle);
    buf[1] = wiringPiI2CRead(handle);
    Temp = (buf[0] << 4) | (buf[1] >> 4);

    if(Temp > 0x7FF)
    {
        Temp = (~Temp) & 0xFFF;
        Temp++;
        temperature = -Temp * LSB;
    }
    else
        temperature = Temp * LSB;
    return(temperature);
}

// Start of MAIN program. Read the temperature and send to Android
// smartphone when request character T is received
//
int main(void)
{
    int sock, len, num, temperature;
    struct sockaddr_in serveraddr, clientaddr;
    struct tm tm_now;
    char timbuff[100];
    char tmp[50];

    wiringPiSetupGpio();
    handle = wiringPiI2CSetup(DeviceAddress);

    sock = socket(AF_INET, SOCK_DGRAM, 0);
    len = sizeof(clientaddr);

    serveraddr.sin_family = AF_INET;
    serveraddr.sin_addr.s_addr = INADDR_ANY;
    serveraddr.sin_port = htons(Port);
    bind(sock,(struct sockaddr *)&serveraddr, sizeof(serveraddr));

    clientaddr.sin_family=AF_INET;
    clientaddr.sin_addr.s_addr=inet_addr("192.168.1.219");
    clientaddr.sin_port=htons(Port);

    while(1)
    {
        time_t now = time(NULL);
        localtime_r(&now, &tm_now);
        strftime(timbuff,sizeof(timbuff),"%d-%m-%Y %H:%M:%S",&tm_now);
        temperature = (int)ReadTemperature();
        sprintf(&tmp[0], "%d", temperature);
        strcat(timbuff, " ");
        strcat(timbuff, tmp);
        strcat(timbuff, "C");
        sendto(sock, timbuff, strlen(timbuff), MSG_CONFIRM,
               (struct sockaddr *)&clientaddr, len);
        delay(5000);
    }
}
```

图 14.11 程序 TMP102UDP2.c

本项目使用 Wezzi Studios 的 Android 应用 UDP RECEIVE and SEND（见图 14.12）来接收并显示 UDP 数据包。该应用可在 Play Store 上免费获取。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_338_0.png)

图 14.12 UDP RECEIVE and SEND 应用

图 14.13 显示了 Android 应用接收到的数据包。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_339_0.png)

图 14.13 Android 智能手机上的示例显示

您可以按如下方式编译并运行程序：

```bash
gcc -o TMP TMP102UDP2.c -lwiringPi
sudo ./TMP
```

## 14.8 ● 项目 5 – Web 服务器应用 – 控制两个 LED

### 描述：
本项目将开发一个 Web 服务器应用，用于控制连接到树莓派的两个 LED。

### 目标：
本项目旨在展示如何开发 Web 服务器应用。

### 框图：
图 14.14 显示了本项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_340_0.png)

图 14.14 项目框图

### 电路图：
本项目的电路图如图 14.15 所示。LED0 和 LED1 分别通过 470 欧姆限流电阻连接到树莓派的 GPIO 21 和 20。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_340_1.png)

图 14.15 系统电路图

### HTTP Web 服务器/客户端
Web 服务器是一种使用 HTTP（超文本传输协议）响应用户请求并向用户提供网页的程序。这些请求由 HTTP 客户端转发。通过使用 HTTP 服务器/客户端对，我们可以通过 Web 控制任何连接到 Web 服务器处理器的设备。

图 14.16 显示了 Web 服务器/客户端设置的结构。图中，树莓派是 Web 服务器，PC（或笔记本电脑、平板电脑或手机）是 Web 客户端。待控制的设备连接到 Web 服务器处理器。在本示例中，我们将两个 LED 连接到树莓派。系统运行如下：

- Web 服务器处于监听模式，监听来自 Web 客户端的请求。
- Web 客户端通过发送 HTTP 请求向 Web 服务器发起请求。
- 作为响应，Web 服务器向 Web 客户端发送 HTTP 代码，该代码由用户在 Web 客户端上的 Web 浏览器激活，并以表单形式显示在 Web 客户端屏幕上。
- 用户发送命令（例如点击 Web 客户端表单上的按钮以点亮 LED），这会向 Web 服务器发送代码，以便 Web 服务器执行所需操作。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_341_0.png)

本程序中，使用 IP 地址为 192.168.1.199 的笔记本电脑作为 Web 客户端。使用 IP 地址为 192.168.1.202 的树莓派作为 Web 服务器。

### 程序清单：
图 14.21 显示了完整程序（程序：WEBSERVER.c）。程序开头包含了所需的库头文件。注意端口号设置为 80，这是默认的 HTTP 端口号。LED0 和 LED1 分别分配到 GPIO 端口编号 21 和 20。

程序随后定义了当请求时要发送到 Web 客户端的 HTML 代码

