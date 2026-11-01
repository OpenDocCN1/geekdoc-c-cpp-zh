# Chapter 10 – RTCC (Real Time Clock Calendar)

In this chapter we will exercise the RTCC (Real Time Clock Calendar) peripheral on the PIC2H. The experiment is recommended for use only with the 16 Bit Micro Experimenter (see appendix A), because all necessary support hardware i.e. clock crystal, LCD, and four pushbuttons are already in place.

# The Real Time Clock Calendar

We have been talking about the Experimenter's clock, so here it is. It is a Real-Time Clock and Calendar (RTCC) function and is intended for applications where accurate time must be maintained for extended periods of time with minimum to no intervention from the CPU. The peripheral is optimized for low-power usage in order to provide extended battery lifetime while keeping track of time. It features a 100-year clock and calendar with automatic leap year detection. The range of the clock is from 00:00:00 (midnight) on January 1, 2000 to 23:59:59 on December 31, 2099. The hours are available in 24-hour (military time) format. The clock provides a granularity of one second.

The RTCC internal register interface with the PIC24H Microcontroller is implemented using the Binary Coded Decimal (BCD) format. This simplifies the software, when reading and writing to the module, as each of the digit values is contained within its own 4-bit value

![](bbox=[0.22, 0.7, 0.8, 0.95])