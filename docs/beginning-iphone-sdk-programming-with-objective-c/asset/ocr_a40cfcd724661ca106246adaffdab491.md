# THE IPHONE SIMULATOR IS NOT AN EMULATOR

The iPhone Simulator is a simulator, not an emulator. So what is the difference? Well, a simulator tries to mimic the behavior of a real device. In the case of the iPhone Simulator, it simulates the real behavior of an actual iPhone device. However, the simulator itself uses the various libraries installed on the Mac (such as QuickTime) to perform its rendering so that the effect looks the same as an actual iPhone. Also, applications tested on the simulator are compiled into x86 code, which is the byte-code understood by the simulator.

In contrast, an emulator emulates the working of a real device. Applications tested on an emulator are compiled into the actual byte-code used by the real device. The emulator executes the application by translating the byte-code into a form that can be executed by the host computer running the emulator.

A good way to understand the subtle difference between simulation and emulation is this: Imagine you are trying to convince a child that playing with knives is dangerous. To simulate this, you pretend to cut yourself with a knife and groan in pain. To emulate this, you hold a knife and actually cut yourself.

![](bbox=[0.13, 0.58, 0.3, 0.9])

FIGURE 1-7

The iPhone Simulator can simulate different versions of the iPhone OS (see Figure 1-8). This capability is very useful if you need to support older versions of the platform as well as testing and debugging errors reported in the application on specific versions of the OS.

![](bbox=[0.5, 0.7, 0.85, 0.85])

FIGURE 1-8