
## 3.1. Overview of the x86 architecture

```
="a"(a1),="d"(d1)
```

The =a and =d are saying that the %eax and %edx registers must be output, using a as code for eax and d as code for edx, as may be verified by checking the documentation. The destinations for the output are given as (a1) and (d1), where a1 and d1 variables of type unsigned int defined in the C or C++ program. In this way, we are able to execute a machine instruction and bring in information into variables that can be accessed within the C or C++ program.

The volatile qualifier allows the compiler not to change the assembly code part of an optimization. In addition, if two inline assembly statements have the volatile qualifier, the compiler will not move the two statements past each other.

In some processors, such as those of the Pentium M family, the Time Counter is incremented every clock cycle. However, the frequency of clock ticks can vary. To decrease energy consumption, computers vary the frequency of clock ticks and the operating voltage. In other processors, such as the Intel Atom, the Time Counter is incremented at a constant rate regardless of the operating voltage and the actual frequency of the clock. The architectural behavior “moving forward” has been stated to be of the latter type.

Between two calls to rdtsc made on the same processor core, the second call is guaranteed to return a higher count. However, rdtsc is not a serializing instruction. In the presence of multiple pipelines and out-of-order scheduling, some instructions that occur after rdtsc may come sooner, although instructions that occur before complete later. However, one does not need to worry too much about possibilities. With careful use, the Time Counter can be used to measure times that take only a few nanoseconds.

It is of course a nuisance if we have to think about machine instructions every time we want to read the use of the Time Counter in a C++ program. A simple C++ class greatly simplifies the use of the Time Counter. The interface of the Timestamp class is given below.

```cpp
class Timestamp{
public:
    Timestamp()};
```

> Processes may be moved from core to core by the operating system. When that happens, the second reading of the Time Counter may be less than the first. See http://en.wikipedia.org/wiki/Time_Stamp_Counter.

```cpp
void tic();
double toc();
```

The entire Timestamp class is defined in the header file Timestamp.hh to avoid function overhead using function inlining. The constructor does nothing. A call to the member function tic() will issue the rdtsc instruction and record the counter in two variables of type unsigned int. A call to the member function toc() will read and return the number of cycles elapsed since the last call to tic() as a double. The calculation to turn the information from the two readings of the Time Stamp Counter into a double is not shown.

The Timestamp class can be used as follows:

```cpp
Timestamp ts;
ts.tic();
//... code to be timed ...
double cycles = ts.toc();
```

The cycles variable will hold the number of cycles between tic() and toc().

## 3.1.4 Cache parameters and the CPUID instruction

The registers on a processor are few in number. Large arrays and other large data structures cannot be stored in their entirety using registers. They are typically stored in memory (DRAM). However, memory is outside the processor chip. Although it takes only a few cycles to operate on registers, it takes a few hundred cycles to fetch a word from memory. To hide the large number of cycles required to access a word from memory, some memory words are cached on the chip itself. Cache memory is organized into several levels.

We will take a closer look at cache memory in the next chapter. Here we will use the cpuid instruction to ask the processor to report information about its cache and give a preliminary idea of cache memory. As we look at assembly code and explore certain facets of the processor, it will help to have some idea of cache memory. Cache influence the performance of nearly every program.

The cpuid instruction can be used to extract a variety of information about the processor. If you type cat /proc/cpuinfo on a Linux computer, the command returns information about the processor's instruction set, power consumption, caches, support for specific technologies, and clock speed. Much of that information is obtained by the operating system using cpuid. the cpuid instruction has a manual of its own. The AMD and Intel processors use different conventions for cpuid.

The inline assembly statement for extracting information about caches using the cpuid instruction is given below. eax, ebx, and ecx must be defined as variables of type unsigned, and must be an integer value.

```asm
asm volatile("cpuid") //instruction
    :="a"(eax), "=b"(ebx), "=c"(ecx)//output list
    :="a"(0x4), "c"(i) //input list
    :edx); //clobber list
```

This inline assembly statement is more complicated than the one we used to read the Time Counter. The instruction, which is given as cpuid, followed by three colons and not just one. We do not need to pass any parameters to the rdtsc instruction and all the data items by the instruction are output to program variables. In the case of the cpuid instruction, we need to leave some data in the registers to tell the cpuid instruction what to do. In addition, not all the data items returned by the cpuid instruction are output to program variables. The syntax of this inline assembly statement is more complicated for these reasons.

The three colons in this inline assembly statement divide the part inside the parentheses into segments. The first segment, which is before the first colon, gives the instruction to be executed. The second, third, and fourth segments give the output list, the input list, and the so-called clobber list, respectively. In this case, the output list specifies the contents of the registers %eax, %ebx, and %ecx, which are indicated by =a, =b, and =c, respectively, must be output to program variables eax, ebx, and ecx, respectively.

The input list specifies that the register %eax must be loaded with the hexadecimal number 04. By loading other codes into %eax, cpuid can be asked to return information about performance counters, processor management, processor name, and other features of the processor. The input list loads the register value i into the %ecx register. A processor typically has multiple levels of cache, and an integer value is loaded into %ecx to tell cpuid which cache it must get information about.

CPUID returns information in four registers: %eax, %ebx, %ecx, and %edx. Of these, only three are output to program variables. We have elected not to output the %edx register. The clobber list, which is the segment following the third and last colon, includes %edx to tell the compiler the instruction will write over that register. That way the compiler knows to not save information in %edx with plans of using it. The registers %eax, %ebx, and %ecx are also clobbered by the cpuid instruction. However, these should not be in the clobber list because the compiler can figure out that they are being clobbered from the input and output segments.

A program that uses the cpuid instruction to extract information about cache memory follows:

```cpp
cout<<"CPUID with code 04h"<<endl;
unsigned int eax, ebx, ecx;
for (int i=0; i++) {
    asm volatile("cpuid\n        ":a" (eax), "b" (ebx), "c" (ecx)\n        ":a" (0x04), "c" (i)\n        ":d" (edx)");
    if((eax&ecx)==0)
        break;
    printf("cache type = %u\n", eax,ebx);
    printf("cache level = %u\n", (eax>>5)&(0x07));
    printf("ways of associativity = %u\n", (ebx>>22)&0xFFF+1);
    printf("physical line partitions = %u\n", (ebx>>12)&0x3FF+1);
    printf("cache line size = %u\n", (ebx&0xFFFF)+1);
    printf("number of sets = %u\n", ecx+1);
    printf("cache size in bytes = %u\n", ((ebx>>22)&0xFFF+1)*ways of associativity
((ebx>>12)&0x3FF+1)*physical line partns
((ebx&0xFFFF)+1)*cache line size
(ecx+1)); //number of sets
}
```
