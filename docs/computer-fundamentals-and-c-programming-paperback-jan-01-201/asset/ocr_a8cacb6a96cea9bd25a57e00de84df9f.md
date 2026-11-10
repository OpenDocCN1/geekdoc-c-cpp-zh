![](bbox=[0.197, 0.123, 0.804, 0.419])

**FIGURE 1.1**　Program Transformation Before Execution

However, the programs we write are not the ones that are executed. Why? Computers, being binary devices, understand only *meaningful* sequences of 0s and 1s, commonly called *machine language*. Thus, all instructions and data must be input to the CPU in machine language (0s and 1s). Because humans don’t feel comfortable using this language, we need to use a *programming language*, and the computer world offers a number of them (like C). These languages are mildly similar to spoken languages (like English). They support a very small set of *keywords* and symbols held together by a rigid and unforgiving grammar.

The CPU doesn’t understand programming languages, so every program you write must be translated to its corresponding machine language code before execution. The written program is first saved in a file on the computer’s disk. A separate program, called the *compiler*, translates or compiles this source code to its equivalent *machine code* in binary. As shown in Figure 1.1, it is this code that is eventually executed by the CPU.

The CPU needs adequate memory to run programs. It fetches program instructions and data from memory and writes temporary and final data to memory. Memory can be *volatile* (erased when power is withdrawn) or non-volatile, and the CPU uses the appropriate type depending on how long the data need to be preserved. Some memory is inside the CPU while some are outside it but inside the computer housing. For enabling programs to interact with the external world, computers also use external devices as memory (like the portable hard disk and flash memory).

**Takeaway:** The programs we write using a language like C have to be processed by a compiler program for generation of the corresponding machine code. This code, comprising 0s and 1s, eventually runs on the CPU.