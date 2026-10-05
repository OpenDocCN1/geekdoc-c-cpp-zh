+   A process might have application recovery callback registered with WER. This might then display a clear UI to the user, and restart the process in its current exported state, leading anywhere from a recursive crash/loop to the exception which became swallowed.

+   Likely in a C++-based product, caught by an exception handler as "thrown" by the program itself, once again, might swallow the exception or continue execution in an unsafe manner.

Solving these issues requires a mechanism that can raise an exception that cannot be intercepted by of the process's components outside of the WER service, which must itself be guaranteed to receive this exception. This is where security assertions come into.

# Compiler and OS support

When Microsoft libraries, programs, or kernel components encounter unusual security situations, or when mitigations recognize dangerous violations of security state, they now use a special compiler intrinsic supported by Visual Studio,__fastFail, which takes a parameter as input. Alternatively, they can call a runtime library (Rtl) in RtlFast2, which itself contains a __fastFail intrinsic. In some cases, the WDK or SDK can inline functions that call this intrinsic, such as when using the LIST_ENTRY functions InsertListTail and RemoveListTail. In other situations, the Universal CRT (uCRT) itself that has this intrinsic in its functions. In yet others, APIs will also check when calls are made and may use this intrinsic as.

Regardless of the situation, when the compiler generates code that takes the input, moves it to the RCX (x64) or EAX (x86) register, and then triggers a software interrupt with the number 0x29. (For more information on interrupts, see Chapter 8 in Part 2)

In Windows 8 and later, this software interrupt is registered in the Interrupt Dispatch Table (IDT) by the handler KiRaiseSecurityCheckFailure, which you can verify on your own using the idt 29 command in the debugger. This will (for compatibility purposes) in KiFastFailDispatch dispatch with the STATUS_STACK_BUFFER_OVERRUN status (0xC0000049). This will then do kernel exception dispatching through KiDiDispatchException, but that as a second-chance exception, which means the debugger and process will not be notified.

This condition will be specifically recognized and an error message will be sent to the WER error ALPC port as usual. WER will claim the exception as non-continuable, which will cause the kernel to terminate the process with the usual TerminateProcess system call. Therefore, guarantees that once the interrupt is used, no return to user mode will ever be performed in this process again, that WER will be notified, and the process will be terminated (additionally, the error code will be from the exception code). When the exception record is generated,

Kernel-mode code can also raise exceptions, but in this case KiBugCheckDispatch will be called instead, which will result in a special kernel mode crash (bugcheck) with code 0x139 (KERNEL_SECURITY_FAILURE), where the first argument will be the input parameter to __fastFail.