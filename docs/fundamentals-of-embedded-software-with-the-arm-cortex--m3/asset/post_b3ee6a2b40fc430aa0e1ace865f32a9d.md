
## 8.1.2 Thread and Handler Modes

The Cortex-M3 processor operates in one of two modes. During the execution of the main program or a thread, the processor is in *thread mode*; during the execution of a handler the processor is in *handler mode*. When executing code, this “Dr. Jekyll and Mr. Hyde” behavior allows the processor to behave one way for a regular C function and a somewhat different way for a handler. Thread mode and handler mode are distinguished by bits 0 to 8 of the processor status word (PSR). In thread mode, these bits are all zeroes; in handler mode, they hold a nonzero number that identifies the exception type.

## 8.1.3 Entering the Exception Handler

When an exception is recognized by the processor, it automatically responds with a specific sequence of actions:

- 1. **Stacking:** The contents of R0 to R3, R12, the return address, and the contents of the PSR and link register (LR) are pushed onto the stack. (Note that the PSR and registers R0 to R3 and R12 are exactly those registers that the AAPCS¹ does not require functions to preserve.)

- 2. In parallel with the stacking operation, the processor identifies the exception, records its identity as an exception number in the PSR, and uses that number to locate and copy the starting address of the corresponding handler from the *vector table*² into the program counter (PC).

![](img/f0b8aa873b11dc585ed698a10d04e7a7_160_0.png)

FIGURE 8-2 Processor state saved during stacking.

¹The ARM Architecture Procedure Call Standard (AAPCS) is defined in Chapter 7.

²By default, the vector table is stored starting at address 0 but may be relocated by changing the contents of the vector table offset register.

- 3. Register LR is loaded with all 1's except for the least significant 4 bits; these bits record the mode of the processor (thread or handler) prior to the exception. (Note: LR does not contain the return address!) The value stored in LR (known as EXC_RETURN) is a special value recognized and used by the processor to restore the previous mode when the handler returns.)

- 4. Handler mode is enabled.

- 5. Execution of the handler begins.

## 8.1.4 Returning from the Exception Handler³

(The processor initiates the return sequence when the handler executes an instruction (such as “BX LR”) that loads the PC with the EXC_RETURN value. That value signals the processor to start the return sequence and determines whether the processor returns to thread or handler mode. The return sequence then pops eight words from the stack, using them to restore registers R0 to R3, R12, LR, and the PSR, and to load the PC with the return address.)

![](img/f0b8aa873b11dc585ed698a10d04e7a7_161_0.png)

FIGURE 8-3 Hardware interrupt processing.

³ Some exceptions are so serious as to be fatal, so that there is no reason for the handler to return.

## 8.1.5 Latency Reduction

The Cortex-M3 uses three techniques to reduce interrupt latency—the time from the interrupt request until the corresponding handler begins to execute.

### Suspending or abandoning instruction execution

When an interrupt request arrives, the processor is likely to be in the middle of executing an instruction. That instruction is allowed to complete if it can do so in a single clock cycle. Instructions such as LDM, STM, PUSH, and POP that transfer multiple words to or from memory can be suspended and continued after the interrupt. All other instructions are abandoned and restarted after the interrupt so that in all cases the exception request is processed within a single processor clock cycle.

### Late arrival processing

Suppose the processor has begun an interrupt response sequence only to have another interrupt of higher priority suddenly arrive during the stacking operation. Rather than completing the response and entering the handler for the first interrupt only to have it preempted by the late arriving interrupt of higher priority, the processor will redirect the remainder of the interrupt response so that it handles the late arrival first.

### Tail chaining

The data rate capability of interrupt-driven I/O suffers somewhat from the overhead cost associated with saving and restoring the eight word of processor state information. In most processors, when two ISRs execute back-to-back, the state information is popped off the stack at the end of the first interrupt only to be pushed back onto it at the beginning of the next. The Cortex-M3 completely eliminates this useless pop-push sequence with a technique called tail-chaining, reducing the ISR transition time from 24 clock cycles down to only 6.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_162_0.png)

## 8.1.6 Priorities and Nested Exceptions

Some interrupts are more important than others. For example, when you slam on the brakes in your car, you cannot afford to wait for the processor to finish what it may be working on—even if it is executing an ISR for some other device. It is critical that the antilock braking system start working without delay. Real-time applications like anti-lock braking have hard deadlines, and to ensure that these deadlines are met requires that we assign priorities to interrupts and allow higher-priority interrupts to preempt those of lower priority.

The Cortex-M3 processor incorporates a device called the nested vector interrupt controller (NVIC) that implements a priority system among the various exceptions and interrupts. As shown in Table 8-1, lower numbers are assigned to higher priorities, with interrupts from external devices having lower priority than other kinds of exceptions.

There is special hardware interrupt called the nonmaskable interrupt (NMI) whose purpose is to handle catastrophic events such as an impending power failure or a memory parity failure. It has a priority greater than any other interrupt and cannot be disabled.

Most priority numbers are software configurable from 0 (highest) to 255 (lowest), except those for reset, NMI, and hard faults. Until modified by software, the default priority of any exception whose priority is configurable is 0. If two interrupts are assigned the same priority, the one with the lower interrupt number is treated as having a higher priority.

| Exception Type | Exception # | IRQ # | Priority | Comment |
|---|---|---|---|---|
| Reset | 1 | | -3 (fixed) | Initial SP value (loaded on reset) |
| NMI | 2 | | -2 (fixed) | Power up and warm reset |
| Hard fault | 3 | | -1 (fixed) | NMI |
| Memory mgmt. | 4 | | | |
| Bus fault | 5 | | | Address/memory-related faults |
| Usage fault | 6 | n/a | | Undefined instruction |
| Reserved | 7–10 | | Configured through system handler priority registers | |
| SVCall | 11 | | | Software interrupt (SVC instruction) |
| Debug monitor | 12 | | | |
| Reserved | 13 | | | |
| PendSV | 14 | | | |
| SysTick | 15 | | | System timer tick |
| Ext. interrupts | 16–255 | 0–239 | Configurable | |

Priority numbers for the twelve system exceptions (4–15) are stored one per byte in the NVIC, starting at address E000ED18₁₆, and can be modified by code equivalent to:

```
((uint8_t *) 0xE000ED18)[exception_number - 4] = priority ;
```

Priority numbers for up to 240 external interrupts are also stored one per byte in the NVIC, starting at address E000E400₁₆, and can be modified by code equivalent to:

```
((uint8_t *) 0xE000E400)[IRQ_number] = priority ;
```

Once configured, the priority numbers determine which exceptions can preempt the handlers for other exceptions. For example, if the processor is executing the handler for an external interrupt, that handler can be preempted by a hard fault exception because it has a higher priority.

### Enabling and disabling external interrupts

Interrupts can be either entirely or selectively enabled or disabled. To enable or disable all external interrupts, use one of the following two instructions:

- CPSIE i ; Enable external interrupts
- CPSID i ; Disable external interrupts

Individual external interrupts are controlled by two sets of eight registers within the NVIC, called the set enable registers (starting at address E000E100₁₆) and clear enable registers (starting at address E000E180₁₆). Each register is 32 bits wide, with 1 bit per interrupt. Setting a bit to 1 in a set enable register will enable the corresponding interrupt, while setting the corresponding bit to 1 in a clear enable register will disable it. For example, an individual interrupt can be enabled in the NVIC by code equivalent to:

```
((uint32_t *) 0xE000E100)[IRQ_number / 32] |= 1 << (IRQ_number % 32) ;
```

## 8.2 SYNCHRONIZATION, TRANSFER RATE, AND LATENCY

The CPU and I/O devices are physically independent. Events occurring within an I/O device that determine when data is available for input or when the device is ready to receive output data are not under the control of the computer. To transfer data to or from an I/O device requires synchronizing the CPU to the I/O device by somehow checking the status of the device and waiting until it is ready to transfer.

Transfer rate is simply a measure of the number of bytes per second transferred between the CPU and an external device. The fastest transfer rates are provided by direct memory access (DMA), but at the expense of some additional hardware complexity. Polled waiting loops are the easiest to implement and provide good transfer rates but are rarely used in real-time applications. Interrupt-driven I/O is the slowest due to the overhead of saving and restoring the machine state (especially if only 1 byte of data is transferred per interrupt) but is the most commonly used technique of the three.
