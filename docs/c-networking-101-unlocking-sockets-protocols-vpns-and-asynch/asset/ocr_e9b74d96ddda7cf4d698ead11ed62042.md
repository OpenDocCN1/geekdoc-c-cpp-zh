# General Practices for Programming Wireless Networks

Programming a wireless network using C++ involves interaction with the Network Interface Card (NIC) and the networking stack of the operating system. On a Linux platform, we usually use system and networking libraries such as NetworkManager and WPA Supplicant. But for this demonstration, let us focus on the 'iw' command for simple tasks and use system calls in C++.

Below are some general steps for working with wireless networks from a C++ application on a Linux platform:

# Scan Available Networks

First, we will create a simple C++ program to execute a shell command using system calls and fetch the output. Let us take an example of scanning for available networks. You could use the 'iw' command for this.

```
#include
```

```
#include // system, NULL, EXIT_FAILURE
```