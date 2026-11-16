The first stack push stores a value into address SP-4, thus the expression “(unsigned long) pulStack + sizeof(pulStack)” yields the address of the 32-bit word located immediately above the stack.

# 13.3 C RUN-TIME ENVIRONMENT

Once the processor is up and running but before execution enters function main, the startup function must initialize the content of the initialized statics (data) and uninitialized statics (bss) that are located in read/write memory.

# 13.3.1 Copying Initial Values from Nonvolatile Memory into the Data Region

All static variables (which implicitly include all global variables) must be initialized by the startup function. Those statics whose initial values were specified in their declaration reside as a single contiguous group in the “data” region; the constants that are their initial values reside as a corresponding but separate contiguous group in the text region of nonvolatile memory. Before entering function main, the startup function must copy these constants into their respective destinations in the data region of read/write memory. The startup function used by programs created with the IAR Embedded Workbench IDE looks like the following:

```
unsigned long *pulSrc, *pulDest, *pulEnd;
//
// Copy the data segment initializers from flash to SRAM.
//
pulSrc = __segment_begin("DATA_ID");
pulDest = __segment_begin("DATA_I");
pulEnd = __segment_end("DATA_I");
while(pulDest < pulEnd)
{
    *pulDest++ = *pulSrc++;
}
```

In addition to initializing the data section by copying from nonvolatile memory, it may also be desirable on some MCUs to copy the program code to read/write memory because the access time for nonvolatile memory is often somewhat slower than that for read/write memory.

# 13.3.2 Zeroing Uninitialized Statics

There is a convention in C that uninitialized statics in the bss region of memory are filled with zeroes during startup. This region includes all static objects that were declared without specifying an initial value. Since some programs contain code that depends on this

2. “__segment_begin()” and “__segment_end()” are used in IAR’s Embedded Workbench to provide the address of the first byte and byte after, respectively, of the segment specified by the argument: “DATA_ID” refers to the constants in nonvolatile memory that are the initial values of the initialized statics (data); “DATA_I” refers to the segment in read/write memory where the initialized statics reside.