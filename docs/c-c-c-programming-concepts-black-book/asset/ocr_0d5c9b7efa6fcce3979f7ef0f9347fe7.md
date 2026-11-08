themselves to the undefined instruction vector and store the old content. The instruction handler should examine the undefined instruction to check if it can be emulated at all. If it cannot be emulated, then the emulator must pass it on to the original handler using the vector that was stored when the emulator was installed. When a chain of emulators is exhausted, no further processing of the instruction can take place and the undefined instruction handler should report an error and quit.

# ### Prefetch Abort Handler

When the system does not contain any MMU, Prefetch Abort handlers are used. These handlers simply report the error and quit. Otherwise, the address that caused the Prefetch Abort must be restored into the physical memory. The virtual memory fault for that address can be dealt with the instruction fetch retried. The handler should therefore be returned to the same instruction rather than the following one.

# ### Data Abort Handler

In case there is no MMU in the system, the data abort handler should report the error and return. If there is an MMU in the system, then the handler should deal with the virtual memory fault. Three types of instructions cause an abort: Single Register Load or Store, Swap, and Load/Store Multiple.

For the Single Register Load or Store instruction, the response can depend on the type of the ARM processor. If it is an ARM6 processor, then an abort can take place. If the processor is in early abort mode and write-back was requested, then the address register will not be updated. Abort can also happen if the processor is in late abort mode and write-back was requested. In that case, the address register will be updated and the changes must be undone. For an ARM7-based processor, if the abort takes place, then the address register will be updated and the changes must be undone. For processors, such as ARM9TDMI, the address is restored by the processor to the value it had before the instruction started.

For the Swap instruction, no address register update is involved.

For the Load/Store Multiple instruction, the response depends on the processor type. If the processor type is ARM6 or ARM7 and write-back was enabled, then the base register will be updated as if the whole transfer had taken place. For processors, such as ARM9TDMI, the base register will be restored to the value it had before the instruction started.

In each of the three instructions, the MMU can load the required virtual memory into physical memory. The MMU Fault Address Register (FAR) contains the address that caused the abort. When this is done, the handler can return and try to execute the instruction again.

With this, we come to the end of the chapter; let's now summarize the main points discussed in the chapter.

# ## Summary

In this chapter, we have learned about interrupt handling, re-entrant interrupt handlers, and some useful signals. We have also learned how to call subroutines from interrupt handlers. Next, we have learned about Interrupt Service Routines and their implementation using C. In addition, the chapter has discussed how to block signals as well as how exceptions and interrupts are handled by ARM processors.

# ## Quick Revise

# ### Multiple Choice Questions

+   Q1. Which of the following is also known as interrupt signal?
+       i. SIGTERM
+       ii. SIGINT
+       iii. SIGCONT
+       iv. None of the above