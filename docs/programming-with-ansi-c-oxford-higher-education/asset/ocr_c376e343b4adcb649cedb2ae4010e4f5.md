![](bbox=[0.05, 0.12, 0.48, 0.27])

Fig. 13.1 Request for I/O and its reply

involved in the operation, and thus, they are not discussed. Since we have already learnt about streams, there is no need for further exploration of that topic.

Figure 13.1 illustrates how a request from a C++ program for I/O travels via the OS and the device driver to the actual device and how reply comes back traversing the reverse path.

There is one more player in the whole process, which is not shown in Fig. 13.1. A C++ program generally does not request directly to the OS. It invokes an I/O function from a standard library. The standard library comes with the C++ compiler and is made available when C++ is installed. This I/O function, in turn, invokes the request to the OS and passes on the request back to the program when the reply comes back.

The standard library and the I/O functions make the programmer’s job easy. One has to call fopen() to open the file (or .open in C++, which we will study in Section 13.2). The function fopen() is from the standard library, which manages all the complexities. The programmer need not worry about using any OS interface, which is usually far more complex than using standard library functions such as fopen() and fclose(). There is one more reason for this indirection. It makes the program more portable. The function fopen() is found wherever C is installed and .open is available when C++ is installed.

If the OS changes, the implementation of fopen() (the way fopen() is programmed; it may be in assembly language) may be different, but the way it is called remains the same, that is, the program need not change when it runs under a different OS.

Note As a programmer, we cannot have direct control over an I/O device for reading and writing. This is for our own benefit. How? It is because devices and their drivers keep changing, and it is up to the driver designer to ensure compatibility with existing programs. As a result, we do not have to alter an existing program to suit the current requirements of an upgraded driver.

# 13.2 PROCESS OF INPUT/OUTPUT

The devices perform I/O operations under the control of device drivers, which accept commands from the OS. If a programmer wants to perform I/O operations using a device, it is imperative that he/she requests the OS for the same. See Fig. 13.2.

Since different OSs employ different mechanisms to provide I/O, it is very hard to provide a unique I/O standard for all C++ compilers. This standardization is achieved by providing standard I/O libraries. The C++ programmer views the interface provided by the I/O library and not its implementation. A programmer will look at the functions such as fwrite(), fread(), fopen(), and fclose() and not how these functions actually communicate with the OS.

Note Functions such as cin.getline() and cin.read() are very easy to use. The design of a library tries to hide the OS-dependent details deep into implementation. For example, when cin.getline() is used, the programmer is not aware of how cin.getline() function is written. The getline() function in VC++ is coded in a different way than in GNU C++ (Linux). A simple rule of thumb is the more the efforts towards standardizing the library function calls, the easier it is for the programmer. The same C++ program should work with all the compilers. The C++ standard I/O library is a step in that direction.