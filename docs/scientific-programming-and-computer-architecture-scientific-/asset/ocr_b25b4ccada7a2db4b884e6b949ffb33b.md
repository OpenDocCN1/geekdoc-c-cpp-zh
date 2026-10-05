# 3.1. Overview of the x86 architecture

support for specific technologies, and clock speed. Much of that information is obtained by the operating system using cpuid. the cpuid instruction has a manual of its own. The AMD and Intel processors use different conventions for cpuid.

The inline assembly statement for extracting information about caches using the cpuid instruction is given below. eax, ebx, and ecx must be defined as variables of type unsigned, and must be an integer value.

```
asm volatile("cpuid") //instruction
    :="a"eax), "=b"ebx), "=c"ecx)//output list
    :="a"(0x4), "c"i) //input list
    :edx); //clobber list
```

This inline assembly statement has more complicated than the one we used to read the Time Counter. The instruction, which is given as cpuid, followed by three colons and not just one. We do not need to pass any parameters to the rtdsc instruction and all the data items by the instruction are output to program variables. In the case of the cpuid instruction, we need to leave some data in the registers to tell the cpuid instruction what to do. In addition, not all the data items returned by the cpuid instruction are output to program variables. The syntax of this inline assembly statement is more complicated for these reasons.

The three colons in this inline assembly statement divide the part inside the parentheses into segments. The first segment, which is before the first colon, gives the instruction to be executed. The second, third, and fourth segments give the output list, the input list, and the so-called clobber list, respectively. In this case, the output list specifies the contents of the registers %eax, %ebx, and %ecx, which are indicated by =a, =b, and =c, respectively, must be output to program variables eax, ebx, and ecx, respectively.

The input list specifies that the register %eax must be loaded with the hexadecimal number 04. By loading other codes into %eax, cpuid can be asked to return information about performance counters, processor management, processor name, and other features of the processor. The input list loads the register value i into the %ecx register. A processor typically has multiple levels of cache, and an integer value is loaded into %ecx to tell cpuid which cache it must get information about.