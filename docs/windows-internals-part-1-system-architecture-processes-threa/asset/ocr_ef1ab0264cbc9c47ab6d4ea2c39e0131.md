equals 1,024 PB, or 1,048,576 TB), but 64-bit hardware limits this to smaller values. The unmapped region marked in figure 1-5 is much larger than the possible mapped region (about one million times larger on Windows 8), which means the images are (by far) not scale.

![](bbox=[0.166, 0.126, 0.7, 0.373])

FIGURE 1-5 Address space layouts for 64-bit Windows.

Details of the implementation of the memory manager, including how address translation and how Windows manages physical memory, are described in Chapter 5.

# Kernel mode vs. user mode

To protect user applications from accessing and/or modifying critical OS data, Windows uses two processor access modes (even if the processor on which Windows is running supports than two): *user mode* and *kernel mode*. User application code runs in user mode, whereas OS code (such as system services and device drivers) runs in kernel mode. Kernel mode refers to a mode of execution in a processor that grants access to system memory and all CPU instructions. Some processors differentiate between such modes by using the term *code privilege level* or *ring level*, while others use terms such as *supervisor and application mode*. Regardless of what it is, by providing the system kernel with a higher privilege level than user mode applications, the processor provides a necessary foundation for OS designers to ensure that a misbehaving application can't disrupt the stability of the system as a whole.

> The architectures of the x86 and x64 processors define four privilege levels (rings) to protect system code and data from being overwritten inadvertently or maliciously by code of lesser level. Windows uses privilege level 0 (or ring 0) for kernel mode and privilege level 3 (or ring 3) for user mode. The reason Windows uses only two levels is that some hardware architectures, such as ARM today and MIPS/Alpha in the past, implemented only two privilege levels. Settling on the lowest minimum allowed for a more efficient and portable architecture, especially as the other x86/x64 rings do not provide the same guarantees as the ring 0/ring 3 divide.