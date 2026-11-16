Priority numbers for the twelve system exceptions (4–15) are stored one per byte in the NVIC, starting at address E000ED18₁₆, and can be modified by code equivalent to:

```
((uint8_t *) 0xE000ED18)[exception_number - 4] = priority ;
```

Priority numbers for up to 240 external interrupts are also stored one per byte in the NVIC, starting at address E000E400₁₆, and can be modified by code equivalent to:

```
((uint8_t *) 0xE000E400)[IRQ_number] = priority ;
```

Once configured, the priority numbers determine which exceptions can preempt the handlers for other exceptions. For example, if the processor is executing the handler for an external interrupt, that handler can be preempted by a hard fault exception because it has a higher priority.

# Enabling and disabling external interrupts

Interrupts can be either entirely or selectively enabled or disabled. To enable or disable all external interrupts, use one of the following two instructions:

+   - CPSIE i ; Enable external interrupts
+   - CPSID i ; Disable external interrupts

Individual external interrupts are controlled by two sets of eight registers within the NVIC, called the set enable registers (starting at address E000E100₁₆) and clear enable registers (starting at address E000E180₁₆). Each register is 32 bits wide, with 1 bit per interrupt. Setting a bit to 1 in a set enable register will enable the corresponding interrupt, while setting the corresponding bit to 1 in a clear enable register will disable it. For example, an individual interrupt can be enabled in the NVIC by code equivalent to:

```
((uint32_t *) 0xE000E100)[IRQ_number / 32] |= 1 << (IRQ_number % 32) ;
```

# 8.2 SYNCHRONIZATION, TRANSFER RATE, AND LATENCY

The CPU and I/O devices are physically independent. Events occurring within an I/O device that determine when data is available for input or when the device is ready to receive output data are not under the control of the computer. To transfer data to or from an I/O device requires synchronizing the CPU to the I/O device by somehow checking the status of the device and waiting until it is ready to transfer.

Transfer rate is simply a measure of the number of bytes per second transferred between the CPU and an external device. The fastest transfer rates are provided by direct memory access (DMA), but at the expense of some additional hardware complexity. Polled waiting loops are the easiest to implement and provide good transfer rates but are rarely used in real-time applications. Interrupt-driven I/O is the slowest due to the overhead of saving and restoring the machine state (especially if only 1 byte of data is transferred per interrupt) but is the most commonly used technique of the three.