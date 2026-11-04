
- 5. 向客户端发送回复，或关闭套接字。
- 6. 返回步骤 3（如果尚未关闭）。

## 客户端

- 1. 创建 UDP 套接字。
- 2. 向服务器发送消息。
- 3. 等待直到收到服务器响应。
- 4. 处理回复。
- 5. 返回步骤 2，或关闭套接字。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_325_0.png)

图 14.1 UDP 通信

## 14.4 • 项目 1 – 使用 UDP 与 Android 智能手机通信
（树莓派为服务器）

### 描述：

本项目使用 UDP 通信与 Android 智能手机之间接收和发送数据。在本项目中，树莓派是服务器，Android 智能手机是客户端。

### 目标：

本项目旨在展示如何在树莓派与 Android 智能手机之间建立 UDP 通信。

### 框图：

图 14.2 显示了项目的框图。树莓派和 Android 智能手机通过 Wi-Fi 路由器链路通信。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_326_0.png)

图 14.2 项目框图

### 程序清单：

程序清单如图 14.3 所示（程序：**MyServer.c**）。程序开头包含了所需的头文件。消息 **Hello from Raspberry Pi** 存储在字符数组 **msg** 中。然后通过调用 **socket** 函数创建 UDP 类型套接字，并将句柄保存在 **sock** 变量中。接着给出服务器计算机（树莓派）的详细信息，其中地址设置为 **INADDR_ANY**，因此同一网络上端口号设置为 5000 的任何其他计算机都将与树莓派建立通信。然后通过调用 **bind** 函数将服务器计算机的详细信息绑定到指定端口。

程序的其余部分在一个循环中运行。在此循环内，调用 **recvfrom** 函数等待接收来自客户端计算机（Android 智能手机）的数据包。注意这是一个阻塞调用，该函数将一直等待，直到从客户端收到数据。如果从客户端计算机收到字符 **x**，程序终止。向接收到的数据添加一个 NULL 字符，并使用 **printf** 函数将其作为字符串显示在树莓派的 PC 屏幕上。将名为 **count** 的整型变量转换为字符，并添加到字符数组 **msg** 的末尾。该内容被发送到客户端计算机。第一次循环时，客户端计算机将显示 **Hello from Raspberry Pi 1**。第二次时，客户端计算机将显示 **Hello from Raspberry Pi 2**，依此类推。在程序终止前关闭套接字。该程序可按如下方式编译和运行：

```c
gcc -o MyServer MyServer.c
sudo ./MyServer
```

```c
/*--------------------------------------------------------------------------------
        RASPBERRY PI - ANDROID SMARTPHONE COMMUNICATION
        ===============================================

This is UDP program. The program receives and then sends messages to
a smartphone over the UDP socket. Program terminates when character x
is sent from the smartphone

This is the UDP server program, communicating over port 5000

Author: Dogan Ibrahim
File  : MyServer.c
Date  : December 2020
--------------------------------------------------------------------------------*/

#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#define Port 5000
#define BUFFSIZE 1024

// Start of MAIN program
//
int main(void)
{
    int sock, len, num, count = 1;
    char buffer[BUFFSIZE];
    struct sockaddr_in serveraddr, clientaddr;
    char msg[26] = "Hello from Raspberry Pi  ";

    sock = socket(AF_INET, SOCK_DGRAM, 0);
    len = sizeof(clientaddr);

    serveraddr.sin_family = AF_INET;
    serveraddr.sin_addr.s_addr = INADDR_ANY;
    serveraddr.sin_port = htons(Port);
    bind(sock,(struct sockaddr *)&serveraddr, sizeof(serveraddr));

    while(1)
    {
        num = recvfrom(sock, buffer, BUFFSIZE,MSG_WAITALL,
               (    struct sockaddr *)&clientaddr, &len);
        if(buffer[0] == 'x')break;
        buffer[num] = '\0';

printf("%s\n",buffer);

sprintf(&msg[24], "%d",count);
count++;
sendto(sock, &msg, strlen(msg), MSG_CONFIRM,
    (struct sockaddr *)&clientaddr, len);
}
close(sock);
}
```

图 14.3 MyServer.c

Play Store 上有许多免费可用的 UDP 应用。本项目使用 mightyIT 的 UDP Terminal（见图 14.4）。输入你的 Android 智能手机的端口号和 IP 地址，并如图 14.5 所示单击 Start Terminal。程序运行示例如图 14.6 所示，其中同时显示了智能手机和 PC 屏幕。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_328_0.png)

图 14.4 Android 智能手机上的 UDP Terminal 应用

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_328_1.png)

图 14.5 输入端口号

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_329_0.png)

图 14.6 程序运行示例

**注意：** 你可以使用 **ifconfig** 命令查找树莓派的 IP 地址。

## 14.5 • 项目 2 – 将温度读数发送到 Android 智能手机
（树莓派为服务器）

### 描述：

本项目将 TMP102 温度传感器芯片（见第 7 章）连接到树莓派。当智能手机发出请求时，环境温度读数会发送到 Android 智能手机。智能手机通过 Wi-Fi 链路使用 UDP 协议向树莓派发送字符 T 来发出请求。发送字符 x 会终止程序。

### 目标：

本项目旨在展示如何使用 UDP 协议通过 Wi-Fi 链路将温度读数发送到 Android 智能手机。

### 框图：

图 14.7 显示了项目的框图。本项目使用 TMP102 模块（见图 7.16）。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_330_0.png)

图 14.7 项目框图

### 电路图：

项目的电路图如图 7.18 所示。TMP102 的 I2C 总线线路具有片上上拉电阻。TMP102 的 I2C 总线线路 SDA 和 SCL 引脚分别连接到 GPIO 2 和 GPIO 3。

### 程序清单：

图 14.8 显示了程序清单（程序：TMP102UDP.c）。本程序使用 wiringPi 库和 GPIO 引脚编号。程序分为两部分：从 TMP102 读取温度的函数，以及将温度读数发送到 Android 智能手机的主程序。函数 ReadTemperature 从 TMP102 传感器模块读取温度，并以浮点数形式返回给主程序（详细信息见第 7.5 节）。主程序在一个循环中运行，等待接收来自 Android 智能手机的命令。如果收到的命令是字符 x，程序终止，并向智能手机发送消息“程序结束”。如果命令是 T，则调用函数 ReadTemperature。温度被转换为整数并存储在变量 temperature 中。然后将其转换为字符串并存储在数组 msg 中。随后将字符 C（摄氏度）添加到 msg 末尾，并发送到 Android 智能手机上显示。如果用户命令不是 x 或 T，则发送错误消息“错误——应为 T 或 x”，并显示在 Android 屏幕上。你可以按如下方式编译和运行程序：

```c
gcc -o TMP102UDP TMP102UDP.c -lwiringPi
sudo ./TMP102UDP
```

```c
/* SENDING TEMPERATURE TO ANDROID SMART PHONE

In this program a TMP102 type temperature sensor chip is connected to Raspberry Pi. The program sends the temperature reading to an Android smartphone when a request is made. A request is made when the smartphone sends character T to Raspberry Pi over a Wi-Fi link. Sending character x terminates the program. Any other character generates an error message on the Android screen

This is the UDP server program, communicating over port 5000

Author: Dogan Ibrahim
File : TMP102UDP.c
Date : December 2020
*/

// wiringPi includes and defines
//
#include <wiringPi.h>
#include <wiringPiI2C.h>
#define DeviceAddress 0x48
#define PointerReg 0x00

// UDP includes and defines
//
#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#define Port 5000
#define BUFFSIZE 1024

int handle;

// This function reads the temperature from TMP102 and returns to
// the calling main program as a floating point number
//
float ReadTemperature()
{
    int Temp, buf[2];
    float temperature, LSB = 0.0625;
```
