# Chapter 6

+   - Changes the appropriate CPSR mode bits. This helps in mapping to the appropriate registers as well as disabling interrupts.
+   - Sets the link register to the return address.
+   - Sets the program counter to the address of the branch instruction that is mentioned in the vector table. This branches to the appropriate exception handler.

Similar to entering into an exception, some instructions are executed while leaving an exception. However, the steps for executing such instructions depend on the fact that whether the exception handler has used any stack or not. In both the cases, the exception handler performs the following actions:

+   - Restores the CPSR from SPSR
+   - Restores the program counter by using the return address, which was stored in the link register

When an exception is taken, the actual location pointed to by the program counter depends on the exception type. The program counter may or may not be updated to the next instruction to be fetched because of the way in which the ARM processor fetches instructions when an exception is taken. This means that the return address may not necessarily be the next instruction pointed to by the program counter.

# Installing Exception Handlers

A new exception handler must be installed inside a vector table. After the installation, the new exception handler executes when the corresponding exception occurs. An exception handler is installed by using either the branch instruction or the load pc instruction. By using the branch instruction, each entry inside the vector table contains a branch entry, which points to the required exception handler routine. However, this scheme has a limitation, as it has a range of 32 MB. By using the load pc instruction, the program counter is forced to point to the handler address directly by storing the absolute address of the handler.

# Interrupt Handlers

The ARM processor has two levels of external interrupt: FIQ and IRQ. For an interrupt to be executed, the appropriate disable bit in the CPSR must be clear. FIQ interrupts have a higher priority as compared to IRQ interrupts. Both the external interrupts differ in the following two ways:

+   - FIQs are serviced first when multiple interrupt occurs.
+   - Servicing of FIQs causes IRQs to be disabled. They remain disabled until the FIQs are finished executing and then turned back once again.

Interrupt handlers can be written in C by using the __irq keyword, which cannot be used for the re-entrant interrupt handlers because it does not store all the required states. The irq keyword preserves all other registers (excluding the floating-point registers) used by the interrupt handler function. It exits the function by setting the program counter to the value stored in the link register and restoring the CPSR to its original value. If the function calls a subroutine, __irq preserves the link register for the interrupt mode.

# Reset Handlers

The job performed by a reset handler depends on the operating system platform and the system for which the software is developed. A reset handler might be used for setting up exception vectors. It can be used for initializing stacks and registers as well as the memory system, if it is a Memory Management Unit (MMU). Reset handlers are used for initializing I/O devices and enabling interrupts. They play a major role in changing the mode or state of a processor.

# Undefined Instruction Handler

Instructions that are not recognized by the processor are often given to the co-processor for further execution. If they are still un-recognizable, then an undefined instruction exception takes place. It might happen that the instruction is made for a co-processor, which is currently not attached to the system. In such a scenario, the instruction is passed on to the software emulator for the co-processor. Such emulators should attach