
analog electrical signal. Since the microcontrollers only understand binary numbers, the on-chip ADC of the PIC18F then converts the electrical signal to an 8-bit or 10-bit binary value before processing.

All PIC18F microcontrollers use pipelining to execute instructions. The pipelining is performed in two stages which is defined as a single instruction cycle. The PIC18F microcontrollers use the main oscillators (OSC1) to synchronize its internal operations.

The PIC18F clock input is internally divided by four to generate four non-overlapping clocks (Q1, Q2, Q3 and Q4). A machine cycle is defined as four pulses from the main oscillator (OSC1). During the time Q1 is active in any machine cycle, the program counter is incremented by 2 (since the PIC18F instruction size is normally 16-bit) to point to the next instruction to be fetched. This instruction will be fetched during Q4. Simultaneously, the previous instruction is being executed during the whole machine cycle (from Q1 to Q4).

As mentioned in Chapter 2, there are three phases of an instruction execution. They are fetch, decode, and execution. During the fetching phase, the instruction is fetched from the program memory and stored into the Instruction Register (IR) during Q4. During the decoding phase, the control unit translates the contents of the IR, and determines the specified operation to be performed. Finally, during the execution phase, the microcontroller executes the instruction. The clocks and instruction execution flow are shown in Figure 5.1.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_106_0.png)

| Tcy0 | Tcy1 | Tcy2 | Tcy3 | Tcy4 | Tcy5 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Fetch 1 | Execute 1 | | | | |
| | Fetch 2 | Execute 2 | | | |
| | | | Fetch 3 | Execute 3 | |
| | | | | Fetch 4 | Flush (NOP) |
| | | | | | Fetch SUB_1 | Execute SUB_1 |

- MOV LW 55h
- MOVWF PORTB
- GOTO SUB_1
- BSF status, C (Forced NOP)
- Instruction @ address SUB_1

All instructions are single cycle, except for any program branches. These take two cycles since the fetch instruction is "flushed" from the pipeline while the new instruction is being fetched and then executed.

As mentioned before, the PIC18F uses a two-stage pipeline. This means that execution of the previous instruction is overlapped with fetching of the current instruction. Hence, the PIC18F basically executes instructions in one machine cycle. The basic concepts associated with PIC18F pipelining will be described in the following.

Figure 5.2 shows the PIC18F instruction pipeline flow. Four PIC18F instructions (MOV LW, MOVWF, GOTO, BSF) are used to illustrate the PIC18F pipelining. These instructions are chosen arbitrarily. The meaning of these four instructions are provided below:

- MOV LW 0x55 moves 55 hex (8-bit immediate data) into WREG (Accumulator).
- MOVWF PORTB moves the contents of WREG (Accumulator) into PORTB.
- GOTO SUB_1 unconditionally jumps to address SUB_1.
- BSF STATUS, C sets carry flag in the status register to 1.

In the PIC18F, an “Instruction Cycle” consists of four Q cycles: Q1 through Q4. The instruction fetch and execute cycles are pipelined in such a manner that a fetch takes one instruction cycle, while the decode and execute phases take another instruction cycle. However, due to the pipelining, each instruction effectively is executed in one cycle. If an instruction causes the program counter to change (e.g., GOTO), then two cycles are required to complete the instruction. A fetch cycle begins with the Program Counter (PC) incrementing in Q1. In the execution cycle, the fetched instruction is stored into the Instruction Register (IR) in cycle Q1. This instruction is then decoded and executed during the Q2, Q3 and Q4 cycles. Data memory is read during Q2 (operand read) and written during Q4 (destination write).

The PIC18F executes each instruction in a single cycle, except for any branch instructions. This is explained in the following.

Consider Figure 5.2. The PIC18F fetches MOV LW instruction into IR during Tcy0. The PIC18F executes MOV LW in Tcy1 and also fetches the next instruction, MOVWF in Tcy1. The PIC18F then executes MOVWF in Tcy2 and fetches GOTO instruction into IR in Tcy2. The PIC18F executes GOTO into IR in Tcy3, and also fetches BSF into IR in Tcy3.

The PIC18F unconditionally jumps to address SUB_1, and executes the instruction at address SUB_1. Hence, the pipeline is flushed (NOP) in Tcy4, and the instruction at address SUB_1 is fetched in Tcy4. The instruction at address SUB_1 is executed in Tcy5. Hence, each of the instructions, MOV LW and MOVWF, is executed in a single cycle. The GOTO instruction, on the other hand, takes two cycles since the instruction BSF is flushed from the pipeline while the new instruction at address SUB_1 is fetched and then executed.

In order to illustrate the basic features of Microcontrollers, one of the PIC18F family members such as the PIC18F4321 is used in this book for developing the programming examples and illustrating interfacing techniques with the PIC18F.

## 5.2 PIC18F Register Architecture

In order to program the PIC18F in assembly language, one must be familiar with the registers of the PIC18F. Hence, a description of these registers is provided in this section.

# PIC18F Architecture And Addressing Modes

Figure 5.3 shows the PIC18F CPU registers. All registers in the PIC18F are mapped as addresses in the data memory, and are called SFRs (Special Function Registers). Hence, each register is assigned with a unique 12-bit memory address. We now briefly describe the functions of these registers in the following.

### WREG

The WREG (Working register) is 8-bit wide. This is the PIC18F accumulator, and has its usual meaning. Most arithmetic and logic operations are performed using the WREG.

### SP

The SP (Stack Pointer) register (called STKPTR in the PIC18F) is 8-bit wide. The PIC18F hardware stack is a group of 31 21-bit registers to hold memory addresses. Note that the PIC18F program counter is 21-bit wide. Hence the stack is 21-bit wide. The low five bits of the STKPTR are used to address the stack. The PIC18F hardware stack is accessed from the bottom. Hence, the SP is incremented by 1 after PUSH and decremented by 1 after POP. Example 7.2 illustrates this. Figure 5.4 shows the details of the SP. Note the hardware stack is implemented by Microchip and is independent of the data memory. The PIC18F subroutine CALL and RETURN instructions push and pop the program counter using the hardware stack. The hardware stack is different from the software stack. The hardware stack is designed by the manufacturer, and is normally used by subroutines and interrupts in PIC18F assembly language while the software stack is created by the programmer using pointers and appropriate addressing modes. The software stack is normally used to store local variables.

The 31 stack registers are neither part of program memory nor data memory. As shown in figure 5.4, the low five bits of the SP address the stack. The stack overflow bit

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_108_0.png)

FIGURE 5.3 PIC18F registers

(STKFUL, bit 7) is set to one if more than 31 registers are attempted for pushing addresses onto the stack by the programmer; otherwise, the stack overflow bit is cleared to zero. The stack underflow bit (STKUNF, bit 6), on the other hand, is set to one if more addresses that are stored in the stack are attempted to be popped by the programmer; otherwise, the stack underflow bit is cleared to zero. Bit 5 is not implemented and is read as 0.

### PC

The maximum size of the PIC18F's PC (Program Counter) is 21-bit wide. The size of the PC varies from one PIC18F family member to another. For example, the size of the PC of the PIC18F4321 is 13-bit wide. The PC normally points to the next instruction. As mentioned before, the 21-bit PC provides the PIC18F with direct addressing capability of a maximum of 2MB (2^21) of program memory. Upon hardware reset, the PC is loaded with zero so that the PIC18F CPU fetches the first instruction from address 0.

The 21-bit PC is comprised of three 8-bit registers, namely PCL (PC Low Byte), PCLATH (PC latch High Byte), and PCLATU (PC Latch Upper 5 bits). The 21-bit PC is stored in these registers as follows: bits 0 through 7 in PCL, bits 8 through 15 in PCLATH, and bits 16 through 20 in the low five bits of PCLATU. Registers PCL, PCLATH, and PCLATU are mapped as special function registers in the data SRAM by the PIC18F.

### Table Pointer

The PIC18F uses the 21-bit Table Pointer register as a pointer to a table in program memory for copying bytes between program memory and data memory. This register is mapped by the PIC18F as three 8-bit special function registers in the data SRAM.

### BSR

The BSR (Bank Select Register) is 8-bit wide. The low four bits are used to provide the bank address from 0 to F; upper four bits of BSR are used to provide the upper four bits of a 12-bit address of data memory. BSR is used for directly addressing the data SRAM.

### FSR

The FSR (File Select Register) consists of three 16-bit registers (FSR0, FSR1, FSR2) with the upper four bits of each FSR as zero. The low 12 bits of FSR0, FSR1, or FSR2 are used to hold the 12-bit memory address of the data SRAM. These registers are basically memory pointers. Hence, they are typically used for handling arrays and pointer-based data accessing. The PIC18F indirectly uses these registers to access data in data SRAM. Each of these three registers are divided into two 8-bit registers as follows: FSR0H (high byte of FSR0) and FSR0L (low byte of FSR0), FSR1H (high byte of FSR1) and FSR1L (low byte of FSR1), FSR2H (high byte of FSR2) and FSR2L (low byte of FSR2).

### PRODH / PRODL

Each of the PRODH and PRODL registers is 8-bit wide. The PIC18F has two 8-bit x 8-bit unsigned multiplication instructions providing 16-bit product. The upper byte of the product is stored in the PRODH register while the lower byte of the product is placed in the PRODL register.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_109_0.png)
![](img/5e76fd429fabd2b62e16a7bfd8cf546f_109_1.png)
