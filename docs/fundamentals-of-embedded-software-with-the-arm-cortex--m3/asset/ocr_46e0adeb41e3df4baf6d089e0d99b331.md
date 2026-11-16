9. Which of the following are true statements? (Circle all that apply.)
(a) DMA may occur between any two memory cycles.
(b) DMA may occur between any two assembly language instructions.
(c) DMA may occur between any two C statements.

10. Which of the following registers are pushed on the stack when the Cortex-M3 responds to an interrupt? (Circle all that apply.)
(a) R0
(b) R4
(c) R12
(d) LR
(e) PSR

11. Which of the following provide the index used to retrieve the handler address from the vector table for an external interrupt?
(a) A hard-coded constant built into the CPU
(b) The next instruction in the pipeline
(c) The NVIC

12. Which of the following provide the index used to retrieve the handler address from the vector table for exceptions that are not external interrupts?
(a) A hard-coded constant built into the CPU
(b) The next instruction in the pipeline
(c) The NVIC

13. True/False: Register LR contains the return address during the execution of an event handler.

14. Which of the following reduce the time between two back-to-back exceptions?
(a) Abandoning
(b) Tail-chaining
(c) Late arrival processing

15. Which of the following redirect the exception response sequence?
(a) Abandoning
(b) Tail-chaining
(c) Late arrival processing

16. Which of the following are true? (Circle all that apply.)
(a) The starting address of the vector table is always zero.
(b) The starting address of the vector table is stored in the vector table offset register.
(c) The starting address of the vector table is different for internal versus external interrupts.

17. Assume that an ISR is currently executing and interrupts are enabled. For each of the following, circle the appropriate adjective to indicate when the CPU will respond to a second interrupt:
(a) If the second interrupt is of (lower/higher) priority, then only after the ISR returns.
(b) Immediately if the second interrupt is of (lower/higher) priority.