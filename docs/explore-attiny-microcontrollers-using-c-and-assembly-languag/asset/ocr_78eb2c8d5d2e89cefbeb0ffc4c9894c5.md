# 10.1 Instruction Timing

The time that an instruction takes to execute is determined by the number of clock cycles that a particular instruction takes to execute as well as the frequency that the microcontroller is operating at. Find the number of clock cycles that instructions take to execute on an ATtiny or other 8-bit AVR microcontroller in the AVR Instruction Set Manual. This information can also be found in the Instruction Set Summary section of the datasheet for a particular AVR part or range of parts.

# 10.1.1 AVR CPU Versions

According to the AVR Instruction Set Manual, there are six different versions of the AVR 8-bit CPU, namely AVR, AVRe, AVRe+, AVRxm, AVRxt and AVRrc. These different CPU versions came about because of updates and enhancements to the AVR CPU over a period of time. Some differences in instruction timing exist between some of the different CPU versions. Instruction timing for AVR, AVRe and AVRe+ CPU versions are identical.

ATtiny25/45/85 and ATtiny13(A) microcontrollers fall into the AVR, AVRe and AVRe+ group of AVR CPU versions. It is important to know that there are differences in instruction timing if ever writing software for AVR devices that must run on different AVR CPU versions, if the software relies on the timing of certain instructions.

# 10.1.2 Instruction Timing Examples

Examples of timing for some instructions follow and help to illustrate what instruction timing is about.

# 10.1.2.1 The NOP Instruction

A simple instruction such as the NOP (No Operation) instruction takes one clock cycle to execute on all of the different AVR 8-bit CPU versions. A NOP instruction does nothing, except use up one clock cycle of CPU time. In other words, it does not cause any changes to memory or any registers including the status register.

To work out how much time an instruction takes to execute, we need to find out at what frequency the microcontroller is being clocked, and the number of clock cycles that the particular instruction takes to execute. For the NOP instruction, we know that one clock cycle is used up to execute it. For the ATtiny25/45/85 we know that the default clock frequency is 1MHz and for the ATtiny13(A) the default clock frequency is 1.2MHz.