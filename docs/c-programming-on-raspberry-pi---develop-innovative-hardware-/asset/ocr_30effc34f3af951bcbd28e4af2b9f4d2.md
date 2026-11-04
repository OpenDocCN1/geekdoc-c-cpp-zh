# Block diagram:

Figure 14.2 shows the block diagram of the project. The Raspberry Pi and Android smartphone communicate over a Wi-Fi router link.

![](bbox=[0.291, 0.186, 0.671, 0.399])

Figure 14.2 Block diagram of the project

# Program listing:

The program listing is shown in Figure 14.3 (Program: **MyServer.c**). At the beginning of the program, the required header files are included in the program. The message **Hello from Raspberry Pi** is stored in character array **msg**. A UDP type socket is then created by calling the **socket** function and saving the handle in the **sock** variable. Details of the server computer (Raspberry Pi) are then given where the address is set to **INADDR_ANY** so any other computer on the same network with the port number set to 5000 will establish communication with the Raspberry Pi. The server computer details are then bound to the specified port by calling function **bind**.

The remainder of the program runs in a loop. Inside this loop, function **recvfrom** is called to wait to receive a data packet from the client computer (Android smartphone). Notice this is a blocking call and the function will wait until data is received from the client. The program terminates if character **x** is received from the client computer. A NULL character is added to the received data and is displayed on the PC screen of the Raspberry Pi as a string using the **print** function. An integer variable called **count** is converted into character and added to the end of character array **msg**. This is sent to the client computer. The first time in the loop, the client computer will display **Hello from Raspberry Pi 1**. The second time, the client computer will display **Hello from Raspberry Pi 2** and so on. The socket is closed just before the program terminates. The program can be compiled and run as follows:

```
```c
gcc -o MyServer MyServer.c
sudo ./MyServer
```
```