A Harvard architecture allows program memory and data memory spaces to both start at address 0 as they are separate address spaces. Although the EEPROM on AVR microcontrollers shares the data bus of the data memory or SRAM, it also starts at address 0 because it is accessed as a separate address space using its own set of registers and access protocol.

![](bbox=[0.206, 0.23, 0.853, 0.492])

# 6.4 Fetching and Executing Instructions

All microcontrollers fetch program instructions from memory and execute them. Figure 6.6 shows a simplified block diagram of an AVR microcontroller. Machine language instructions are fetched from Flash program memory into an instruction register and decoded by an instruction decoder. An Arithmetic and Logic Unit (ALU) does mathematical and logic calculations on values in the general purpose registers. All events that occur on a microcontroller are driven by the clock pulse of the microcontroller. If the clock is stopped, the microcontroller no longer fetches and executes instructions.

AVR microcontrollers have an enhancement that improves performance when compared to general microcontrollers discussed so far. A single level pipeline allows the next instruction to be pre-fetched while the current instruction is being executed. By pre-fetching the next instruction while the current instruction is executing, an instruction can be executed in one clock cycle. Figure 6.7 shows how the pipeline improves AVR performance. In a microcontroller without an instruction pipeline the first instruction would be fetched in the first