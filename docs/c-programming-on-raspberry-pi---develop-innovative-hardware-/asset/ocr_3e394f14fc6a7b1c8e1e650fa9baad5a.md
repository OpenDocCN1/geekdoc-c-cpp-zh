called **a.out** in the default directory. For example:

```
    pi@raspberrypi:~$ gcc msg.c
```

+   - Option **-Wall** enables all compiler warnings. For example:

```
    pi@raspberrypi:~$ gcc -Wall -o hello msg.c
```

+   - Option **-S** generates an assembly code listing of the program. In the following example, the assembly listing is stored in file msg.s:

```
    pi@raspberrypi:~$ gcc -S msg.c>msg.s
```

+   - Option **-save-temps** creates executable file (a.out), assembly file, compile file, and list file:

```
    pi@raspberrypi:~$ gcc -save-temps msg.c
    pi@raspberrypi:~$ ls msg.*
    msg.c msg.i msg.o msg.s
```

+   - Option **-l** links with the specified library. In the following example, the code is linked with a library called **wiringPi**:

```
    pi@raspberrypi:~$ gcc -o hello msg.c -lwiringPi
```

+   - Option **-v** displays all the steps gcc takes while compiling the program:

```
    pi@raspberrypi:~$ gcc -v msg.c
```

+   - Option **@** can be used to read the compiler options from a file. For example, assume **MyOptions** contains the lines:

```
    -Wall -o MyOutputFile
```

Then, program **msg.c** can be compiled with the above options as:

```
    pi@raspberrypi:~$ gcc msg.c @MyOptions
```

# 2.6 • Summary

In this chapter, we learned how to develop Python 3 and C programs using several methods. The choice of method for Python depends entirely on the user. In this book, we are interested in developing programs using C. Therefore, the remainder of this book is about the C language and its use with Raspberry Pi.