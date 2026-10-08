# Compiler Security Flags

Compiler flags are options that can be passed to a compiler to customize the compilation process. Security flags specifically aim to enforce stricter code checks, enable additional security features, or emit more secure code.

flag enables stack protection by inserting guard variables—known as stack canaries—into functions, helping to detect and prevent stack buffer overflows.

used with optimization levels higher, this macro provides compile-time checks for buffer overflows in certain functions,

-pie and flags generate Position Independent Code (PIC), which, when used along with ASLR (Address Space Layout Randomization), makes it harder for attackers to predict the memory layout of a process.

-Wformat warning flags help identify potentially hazardous format string usages that could lead to format string vulnerabilities.