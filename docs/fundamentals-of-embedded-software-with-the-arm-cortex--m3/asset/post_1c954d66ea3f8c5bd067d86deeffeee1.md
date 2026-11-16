
```c
char *strtok(char *str1, char *str2) ;
```

The strtok function locates tokens (i.e., substrings) within the string str1. The string str2 defines a set of one or more characters that act as token separators. The following example separates the words of a sentence and prints each word on a line by itself:

```c
char *sentence = "... any English sentence ..." ;
char *word ;

for (word = sentence; word = strtok(word, " ,.;?!") ; word = NULL)
{
printf("%s\n", word) ;
}
```

FIGURE 12-2 Typical usage of the strtok library function.

invocation of strtok to the next, the pointer must use static allocation, and this means that only a single copy of the pointer exists. But this will cause obvious problems when more than one thread tries to use this function!

We now know that library function strtok keeps track of local state information that is used the next time it is called. A sample source-code version of strtok is given in Figure 12-3, showing the use of a static local variable called state to hold this information.

```c
char *strtok(char *string, char *delimeters)
{
static char *state ;
char *beg, *end ;
if (string != NULL) state = string ;
if (state == NULL) return NULL ;
beg = state + strspn(state, delimeters) ;
if (*beg == '\0') return NULL ;
end = strpbrk(beg, delimeters) ;
if (end == NULL) state = NULL ;
else {*end++ = '\0'; state = end; }
return beg ;
}

This local static object causes problems when strtok is called from more than one thread.
```

FIGURE 12-3 Library function strtok with problematic local static object.

A thread-safe (reentrant) version of strtok (called strtok_r) solves the problem by replacing the local static pointer by a thread-specific object created by the caller and accessed by the function via a parameter as shown in Figure 12-4.

```c
char *strtok_r(char *string, char *delimeters, char **state)
{
char *beg, *end ;
if (string != NULL) *state = string ;
if (*state == NULL) return NULL ;
beg = *state + strspn(*state, delimeters) ;
if (*beg == '\0') return NULL ;
end = strpbrk(beg, delimeters) ;
if (end == NULL) *state = NULL ;
else { *end++ = '\0' ; *state = end ; }
return beg ;
}
```

![](img/f0b8aa873b11dc585ed698a10d04e7a7_232_0.png)

FIGURE 12-4 Library function strtok_r replaces local static by a third parameter.

Another example of a library function with similar problems caused by keeping a local static object is the random number generator, rand. A sequence of calls to rand produces a sequence of pseudo-random numbers. A companion function srand initializes the sequence using a starting “seed” value; for any one seed, the sequence of numbers produced by rand is deterministic and thus repeatable. However, if multiple threads call rand (or srand), the sequence returned within any one thread will no longer be deterministic. This may not be acceptable in certain situations.

## 12.4.2 Functions That Return the Address of a Local Static Object

Another coding practice that causes problems in multithreaded programs is the use of functions that return the address of a local static object. An example of such a function is shown in Figure 12-5. This function combines a string and an integer to form a 12-character filename. The filename is prepared in a local static buffer whose address is returned as the value of the function.

Suppose we call this function to prepare a filename to be used in a subsequent file creation. Then, if a second thread calls the same function before we have a chance to create the file, our filename will have been modified.

The problem, of course, is that there is only a single buffer shared by all threads; the solution is to have each thread provide its own separate buffer. In general, there are two ways to accomplish this: (1) let the thread provide the buffer by passing its address as an extra parameter to the function, as shown in Figure 12-6 or, (2) allocate the buffer from the heap, as shown in Figure 12-7.

Allocating from the heap eliminates adding a new function parameter but requires that the programmer release the space by an explicit call to library function free when the filename is no longer needed. Having the caller provide the buffer is faster, since we do not have to search for heap space, and it guarantees that the function will not fail when insufficient heap space is available.

```c
char *Make_Filename(char *name, int version)
{
    static char fname_bfr[13] ;
    sprintf(fname_bfr, "%8s.%03d", name, version) ;
    return fname_bfr ;
}
```

FIGURE 12-5 Example of a function that returns the address of a local static object.

```c
char *Make_Filename(char *name, int version, char *fname_bfr)
{
    sprintf(fname_bfr, "%8s.%03d", name, version) ;
    return fname_bfr ;
}
```

FIGURE 12-6 Function modified to let the caller provide the thread-specific buffer.

```c
char *Make_Filename(char *name, int version)
{
    char *fname_bfr = (char *) malloc(13) ;
    if (fname_bfr == NULL) return NULL ;
    sprintf(fname_bfr, "%8s.%03d", name, version) ;
    return fname_bfr ;
}
```

FIGURE 12-7 Function modified to allocate a thread-specific buffer from the heap.

The standard C library contains several functions that return the address of a local static object. These functions include ctime, asctime, localtime, gmtime, getenv, strerror, and tmpnam. Some C compilers provide special versions of these functions that have been modified for use in multithreaded programs. The modified versions usually have a name that appends "_r" (for reentrant) onto the end of the original name, as in ctime_r.

## 12.5 ACCESSING SHARED MEMORY

Let us suppose we have a program that contains shared memory, and that we have decided that it cannot be avoided. For example, a queue to buffer data from the ISR of an input device is shared memory, even if the program is not multithreaded. So how exactly can the queue data structure get corrupted? And how do we synchronize access to the queue so that it is protected?

![](img/f0b8aa873b11dc585ed698a10d04e7a7_234_0.png)

Consider the code shown in Figure 12-8. On the left is a sequence of instructions in its main program that has removed an item from a queue and is now decrementing its count. On the right is the ISR that enters data into the queue and then increments its count. If the ISR interrupts the main program in the middle of the instruction sequence that decrements the count, then the ISR's incremented count will be over-written when it returns to the main program, and the program will not know that a new item has been added to the queue.

For example, suppose that the initial count of items in the queue is 10. When the main program removes an item from the queue, it starts to decrement the count. It loads the old count (10) into register R1 to begin the decrement sequence but is suddenly interrupted by the ISR before it can go any further. All of the registers (including R1) of the main program are saved on the stack upon entry to the ISR. Then the ISR inserts a new item into the queue and increments the queue count from 10 to 11, restores the registers of the main program (including the value of 10 that was in R1), and returns. The main program resumes where it left off, decrements R1 to R9, and then stores that into count, thus overwriting the value of 11 that was put there by the ISR. Note that there was one queue insertion and one deletion, so the queue count should still be 10 when we are done. But because of the shared memory conflict, the count was left at 9!

### 12.5.1 The Effect of Processor Architecture

The previous example usually applies only to load/store architectures like that of the ARM processor. Other processors often have increment and decrement instructions that can update the count in a single instruction instead of a sequence as shown. Since interrupts occur only _between_ instructions, the decrement of the count would then complete before the interrupt was recognized. However, if the count is kept in a 32-bit integer (such as the timer tick count in the IBM-PC) and if the processor registers are only 8 or 16 bits wide, then more than one instruction would be required to increment or decrement the count. In general, any multi-instruction increment or decrement sequence would have to be protected against interruption. Thus you would have to disable interrupts before the increment or decrement operation, and reenable them after, as shown in Figure 12-9.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_235_0.png)

FIGURE 12-9 Even simple operations in C must be protected against interruption.

As we have just seen, interrupts can occur not only between two lines of C code, but also between any two machine instructions. As shown in Table 12-2, even the simplest line of C code can produce more than one machine instruction, especially when it involves operands whose sizes exceed the capabilities of single instructions. For 16-bit processors this includes longs, pointers, any floating-point data, and most structures. For 8-bit processors we have to also consider all of the 16-bit operands, such as shorts. Rather than worrying about these differences, it is a good programming practice to just protect access to _any_ shared memory—regardless of size. But life is clearly simpler with a 32-bit processor!

ISRs are not the only example of code sequences that execute asynchronously. Preemptive real-time kernels are common in embedded software, and they use ISRs as trigger points to context switch from one thread to another in a multithreaded application. When an interrupt occurs, the ISR may return to a thread other than the one that was interrupted. Since an interrupt can occur at any point during the execution of a thread, all threads are asynchronous with respect to all other threads. As a result, we must worry about objects shared between threads, even if those objects are not accessed by any ISR.
