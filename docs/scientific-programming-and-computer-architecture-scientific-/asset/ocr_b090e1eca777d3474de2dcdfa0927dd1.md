```
void tic();
double toc();
;
```

The entire Timestamp class is defined in the header file Timestamp.hh to avoid function overhead using function inlining. The constructor does nothing. A call to the member function tic() will issue the rdtsc instruction and record the counter in two variables of type unsigned int. A call to the member function toc() will read and return the number of cycles elapsed since the last call to tic() as a double. The calculation to turn the information from the two readings of the Time Stamp Counter into a double is not shown.

The Timestamp class can be used as follows:

```
Timestamp ts;
ts.tic();
//... code to be timed ...
double cycles = ts.toc();
```

The cycles variable will hold the number of cycles between tic() and toc().

# 3.1.4 Cache parameters and the CPUID instruction

The registers on a processor are few in number. Large arrays and other large data structures cannot be stored in their entirety using registers. They are typically stored in memory (DRAM). However, memory is outside the processor chip. Although it takes only a few cycles to operate on registers, it takes a few hundred cycles to fetch a word from memory. To hide the large number of cycles required to access a word from memory, some memory words are cached on the chip itself. Cache memory is organized into several levels.

We will take a closer look at cache memory in the next chapter. Here we will use the cpuid instruction to ask the processor to report information about its cache and give a preliminary idea of cache memory. As we look at assembly code and explore certain facets of the processor, it will help to have some idea of cache memory. Cache influence the performance of nearly every program.

The cpuid instruction can be used to extract a variety of information about the processor. If you type cat /proc/cpuinfo on a Linux computer, the command returns information about the processor's instruction set, power consumption, caches,