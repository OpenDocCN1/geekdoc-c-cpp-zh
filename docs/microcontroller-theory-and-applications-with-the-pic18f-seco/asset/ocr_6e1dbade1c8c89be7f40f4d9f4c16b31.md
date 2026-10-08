# **3.1.1 Main memory**

As mentioned before, the main memory (or simply, the memory) stores both instructions and data. For 8-bit microcontrollers, the memory is divided into a number of 8-bit units called *memory words*. An 8-bit unit of data is termed a *byte*. Therefore, for an 8-bit microcontroller, *memory word* and *memory byte* mean the same thing. For 16-bit microcontrollers, a word contains two bytes (16 bits). A memory word is identified in the memory by an address. For example, the PIC18F is an 8-bit microcontroller, and can directly address a maximum of two Megabytes ($2^{21}$) of program memory space. The data memory address, on the other hand, is 12-bit wide. Hence, the PIC18F can directly address data memory of up to 4kbytes ($2^{12}$). This provides a maximum of $2^{12} = 4096$ bytes of data memory addresses, ranging from 000 to FFF in hexadecimal.

An important characteristic of a memory is whether it is volatile or nonvolatile. The contents of a volatile memory are lost if the power is turned off. On the other hand, a nonvolatile memory retains its contents after power is switched off. ROM is a typical example of nonvolatile memory. RAM is a volatile memory unless backed up by batteries.

Large areas of data memory require an efficient addressing scheme to make rapid access to any address possible. Ideally, this means that an entire address does not need to be provided for each read or write operation. For PIC18F, this is accomplished with a RAM

![](bbox=[0.28, 0.4, 0.57, 0.64])

**FIGURE 3.1** PIC18F data memory.

![](bbox=[0.1, 0.66, 0.9, 0.87])

**FIGURE 3.2** Summary of available semiconductor memories for microcontroller systems.