# Quantum accounting

Each process has a quantum reset value in the process control block (KPROCESS). This value is used when creating threads inside the process and is duplicated in the thread control block (KTHREAD), which is used when giving a new quantum target. The quantum reset value is stored in terms of actual quantum units (we will discuss what these mean soon), which are then multiplied by the number of clock cycles per quantum, resulting in the quantum target.

As a thread runs, CPU clock cycles are charged at different events, such as context switches, interrupts, and server scheduling decisions. If, at a clock interval timer interrupt, the number of CPU clock cycles charged has reached (or passed) the quantum target, quantum end processing is triggered. If there is another thread at the same priority waiting to run, a context switch occurs to the next thread in the ready queue.

Internally, a quantum unit is represented as one-third of a clock tick. That is, one clock tick equals three quantums. On client Windows systems, threads have a quantum reset value of 6 (2 * 3) and server systems have a quantum reset value of 36 (12 * 3) by default. For this reason, KiCyclesPerClockQuantum value is divided by 3 at the end of the calculation previously described, because the original value describes only CPU clock cycles per clock interval timer.

The reason a quantum was stored internally as a fraction of a clock tick rather than an exact tick was to allow for partial quantum decay-on wait completion in versions of Windows prior to Windows Vista. Vista used the quantum timer for expiration. If this adjustment had not been made, it would have been possible for threads to never have their quantums reduced. For example, if a thread entered a wait state, ran, and another entered wait state but never the currently running thread when the clock interval timer fired, it would never have its quantum charged for the time it was running. Because threads now have CPU clock cycles charged instead of quantums, and because this no longer depends on the clock interval timer, these adjustments are not required.

# EXPERIMENT: Determining the clock cycles per quantum

Windows doesn't expose the number of clock cycles per quantum through any function. However, with the calculation and description we've given, you should be able to determine this on your own using the following steps and a debugger like WinDbg in local debugging mode:

+    Obtain your processor frequency as Windows has detected it. You can use the value stored in the PRCB's MHz field, which you can display with the cpuinfo command. Here is a sample output of a four-processor system running at 2794 megahertz (MHz):
1kd> cpuinfo

```
CP F/S Manufacturer MHz PRCB Signature MSR 8B Signature Features
0 66,3 GenuineIntel 2794 fffffffff00000000<ffff a3d3fff
1 66,3 GenuineIntel 2794 fffffffffffffffffff
2 66,3 GenuineIntel 2794 fffffffffffffffffff a3d3fff
3 66,3 GenuineIntel 2794 fffffffffffffffffff a3d3fff
```