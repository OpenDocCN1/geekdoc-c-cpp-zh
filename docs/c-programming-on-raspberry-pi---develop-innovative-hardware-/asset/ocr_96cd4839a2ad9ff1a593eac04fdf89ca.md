# **Circuit diagram:**

The circuit diagram of the project is shown in Figure 12.7. A passive buzzer is connected to pin GPIO 2.

![](bbox=[0.329, 0.187, 0.669, 0.355])

# **Program listing:**

The header file **<softTone.h>** must be included at the beginning of the program in addition to **<wiringPi.h>**. The following functions are provided:

**softToneCreate**: This function creates a software-controlled tone pin. The pin number must be specified as the argument of the function.

**softToneWrite (int pin, int freq)**: This function generates tone with the specified frequency. The first argument of the function is the pin number. The second is the frequency in Hz. Notice the tone is played until the frequency is set to 0.

The program must be compiled using the **lpthread** library in addition to the **wiringPi** library.

Figure 12.8 shows the program listing (Program: **tone1.c**). The program is very simple as it calls the wiringPi functions to generate a 1kHz signal. The program can be compiled and run as follows:

```
```
gcc -o tone1 tone1.c -lwiringPi -lpthread
sudo ./tone1
```
```