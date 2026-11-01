
![](img/910b145bee7ca8076318eafbe6d13997_155_0.png)

## Chapter 9 PWM Schematic
Beginner's Guide to Embedded C Programming Vol 3
C. Helli... | Rev. 1.0 | 9/16/2010 | Page 1 of 1

### Figure 9-1: PWM Project Schematic

The Breadboard setup is shown in Figure 9-2 and has the power from the programmer fed to the rails through two jumpers. The upper rail is ground and the inner rail is V+. The potentiometer plugs right into the breadboard and then the jumper wires provide the power, ground and connection to the AN0 pin.

![](img/910b145bee7ca8076318eafbe6d13997_155_1.png)

### Figure 9-2A: PWM Breadboard Setup

## Software

The full software listing is below. You can see it's very short. The program uses the adcin function along with the pwmout functions in the SimpleC library to create this project.

```
/*********************************
PWM Example
This program reads the value on a potentiometer and drives
the PWM1(CHIPINO pin5/C2) with a duty cycle to match.
It also drives the PWM2(CHIPINO pin6/C1) with a 50% duty cycle
signal.
POT
PIN 1 - Gnd
PIN 2 - CHIPINO Analog pin 0 (AN0)
PIN 3 - 5v

CHIPINO Pin 5 - PWM1 output to 1k resistor
1k resistor to LED Anode
LED Cathode to ground

CHIPINO Pin 6 - PWM2 output to 1k resistor
1k resistor to LED Anode
LED Cathode to ground
*********************************/

#include "simplec1.1.h"

void main(void)
{
init_micro();       // Initialize I/O
char dc = (adcin(0)/10) * 4;  // Convert Pot value to 0-100% Duty Cycle

// **** Both PWM must use the same frequency!******
pwmout1 (dc, 5000);     //Drive variable duty cycle at fixed 5000Hz
pwmout2 (50, 5000);     //Second PWM output 50% Duty Cycle
pause(100);                 // Pause 100msec
}
```

## How it Works

The program begins with a comment block describing the operation and the connections on the breadboard.

```
/*********************************
PWM Example
This program reads the value on a potentiometer and drives
the PWM1(CHIPINO pin5/C2) with a duty cycle to match.
It also drives the PWM2(CHIPINO pin6/C1) with a 50% duty cycle
signal.
POT
PIN 1 - Gnd
PIN 2 - CHIPINO Analog pin 0 (AN0)
PIN 3 - 5v

CHIPINO Pin 5 - PWM1 output to 1k resistor,
1k resistor to LED Anode
LED Cathode to ground

CHIPINO Pin 6 - PWM2 output to 1k resistor,
1k resistor to LED Anode
LED Cathode to ground
*****************************/
```

The first coding step is to include the simplec1.1.h file that has all the SimpleC setup such as configuration bits and some #defines.

```
#include "simplec1.1.h"
```

Now we enter the main loop which starts off by initializing the comparators to off and all the analog pins to digital with the init_micro SimpleC function.

```
void main(void)
{
    init_micro();            // Initialize I/O
}
```

The adcin function is used to read the potentiometer. This function automatically sets the selected pin to analog input mode. In this case it’s AN0 (shown as 0 in the parameter area). This line also shows that you can do operations on the reading prior to storing the result in the variable “dc” which is short for duty cycle. The value we read from the potentiometer will be an 8-bit resolution value of 0 to 255. We need to scale that to 0 - 100 for the pwmout functions so we divide it by 10 (yielding 0 - 25) and then take that result and multiply by 4. This will give us a value of 0 – 100 to be stored in the variable “dc”.

```
char dc = (adcin(0)/10) * 4;  // Convert Pot value to 0-100% Duty Cycle
```

The pwmout functions are number 1 and 2 to control each PWM channel on the CHIPINO module. The PWM peripheral uses the internal Timer 2 clock for controlling the PWM peripheral. Therefore the PWMs must operate at the same frequency. The pwmout1 function uses the “dc” variable as the duty cycle parameter so that variable changes, the duty cycle will change. The frequency is set to 5000 Hz or 5 kHz. The pwmout2 function is set to a fixed 50% duty cycle at 5 kHz. If you look at the oscilloscope plot in Figure 9-3 you can see a frequency reading in the lower right corner. It shows a value of 4.98669 kHz which is real close to 5 kHz so the SimpleC code is working properly.

```
// **** Both PWM must use the same frequency!*****
pwmout1 (dc, 5000);    //Drive variable duty cycle at fixed 5000Hz
pwmout2 (50, 5000);    //Second PWM output 50% Duty Cycle
```

A short pause is added but not really needed. It just delays how often we take the next potentiometer reading.

```
pause(100);            // Pause 100msec
}
```

## Next Steps

There are many ways to take this from here. A real easy change is to adjust the frequency and duty cycle to make sure you understand how the PWM function works. You can also drive more than LEDs with PWM. You can use this to drive a buzzer for noise or use it for controlling the speed of a DC motor if you have the PWM control a transistor that grounds the motor. PWM is very handy and the SimpleC library makes it easy to implement.

The SimpleC calculations are based on a 16 MHz oscillator that runs the CHIPINO module. The PWM peripheral at this clock speed limits the frequency range from 1kHz to 32kHz so you can adjust the frequency parameter from 1000 to 32000. You could do that in a loop to get a variable frequency at a fixed duty cycle. That would be a good project to try on this same setup.

## Chapter 10 – SimpleC Creating Pulses

The PWM function is really useful for continuous frequency outputs, but sometimes you want to create a pulse or burst of pulses and possibly run much slower than the PWM peripheral is capable of. For this reason the pulseout function was created. It is really useful for creating the pulses required to drive a robotic servomotor. In this chapter I’ll show how to use the SimpleC pulseout command to create two pulses that drive a servomotor fully counterclockwise and then fully clockwise. If it’s a continuous rotation servo connected to the wheel of a robot, this project could be used to drive the wheel forward and then backward. This simple motion can be expanded to create a robotic drive routine. Let’s save this for the Next Steps section and just look at the hardware setup.

## Hardware

The hardware used for this project includes a continuous rotation servomotor. Any one will work that can operate at 4.5v. When driving a noisy electrical device like a motor it is best to power the microcontroller separate from the motor. For this reason we use a 4.5v battery pack made from three AA batteries. The servo motor control line is connected to CHIPINO pin 0 (C7 of the PIC16F886). The CHIPINO ground and the 4.5v battery pack ground are connected together to maintain a common reference. The power pin of the servo connector is then connected to the positive lead of the 4.5v battery pack. This is shown in Figure 10-1 as a schematic and then the breadboard setup in Figure 10-2A and 10-2B.

![](img/910b145bee7ca8076318eafbe6d13997_161_0.png)

| Chapter 10 Servo Schematic |  |  |
|---|---|---|
| Beginner's Guide to Embedded C Programming Vol 3 |  |  |
| C. Helli... | Rev. 1.0 | Page 1 of 1 |
|  | 9/16/2018 |  |

Figure 10-1: Servo Motor Schematic

![](img/910b145bee7ca8076318eafbe6d13997_161_1.png)

Figure 10-2A: Servo Motor Breadboard Setup

![](img/910b145bee7ca8076318eafbe6d13997_162_0.png)

Figure 10-2B: CHIPINO Module Breadboard Layout

The software will first create a two millisecond wide pulse on CHIPINO pin 0 that drives the servo counterclockwise. If this is a continuous rotation servo then the wheel connected to the servo will continue to drive counterclockwise while this pulse is present. You can see the pulse on the oscilloscope plot in Figure 10-3.

![](img/910b145bee7ca8076318eafbe6d13997_162_1.png)

Figure 10-3: Two Millisecond Pulse

The software will then create a one-millisecond pulse on the CHIPINO pin 0 to drive the servo in a clockwise rotation thus reversing the wheel. You can see the one-millisecond pulse in Figure 10-4.

![](img/910b145bee7ca8076318eafbe6d13997_163_0.png)

Figure 10-4: One Millisecond Pulse

## Software

The project software is really quite short and simple and I'll go through it in the How it Works section. Here is the total code to drive the servo back and forth. The heart of it is the pulseout command. It's really just a simple high-pause-low routine that creates the pulse, which you can see if you look in the simplec1.1.c file. Always include the simplec1.1.h and simplec1.1.c in your MPLAB project.

```
/***********************
Drive a Servo Motor example using SimpleC.
This code will drive a servo on pin 0 (RC7)
clockwise for a short time, and then
counterclockwise for a short time.

Connections:
CHIPINO PIN 0(RC7) to Servo Signal line
Servo + to 4.5v battery pack
Servo - to Common Ground

Note:
CHIPINO and Battery Pack Grounds are Connected
*************************/
