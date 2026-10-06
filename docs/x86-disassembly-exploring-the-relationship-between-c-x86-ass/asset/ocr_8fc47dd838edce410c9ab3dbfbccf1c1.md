# # 25 Code Obfuscation

# ## 25.1 Code Obfuscation

**Code Obfuscation** is the act of making the assembly code or machine code of a program more difficult to disassemble or decompile. The term 'obfuscation' is typically used to suggest a deliberate attempt to add difficulty, but many other practices will cause code to be obfuscated without being the intention. Software vendors may attempt to obfuscate or even encrypt code to prevent reverse engineering efforts. There are many different types of obfuscations. Notice that many code optimizations (discussed in the previous chapter) have the side-effect of making code more difficult to read, and therefore optimizations act as obfuscations.

# ## 25.2 What is Code Obfuscation?

There are many things that obfuscation could be:

+   - Encrypted code that is decrypted prior to runtime.
- Compressed code that is decompressed prior to runtime.
- Executables that contain Encrypted sections, and a simple decryptor.
- Code instructions that are put in a hard-to-read order.
- Code instructions which are used in a non-obvious way.

This chapter will try to examine some common methods of obfuscating code, but will not necessarily delve into methods to break the obfuscation.

# ## 25.3 Interleaving

Optimizing Compilers will engage in a process called **interleaving** to try and maximize parallelism in pipined processors. This technique is based on two premises:

+   - 1. That certain instructions can be executed out of order and maintain the correct output
- 2. That processors can perform certain pairs of tasks simultaneously.

# ### 25.3.1 x86 NetBurst Architecture

The Intel **NetBurst Architecture** divides an x86 processor into 2 distinct parts: the supporting hardware, and the primitive core processor. The primitive core of a processor