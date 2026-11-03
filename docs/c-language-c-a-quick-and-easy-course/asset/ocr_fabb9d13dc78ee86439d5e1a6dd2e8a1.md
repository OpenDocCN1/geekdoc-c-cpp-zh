# Exclusive directives

The #pragma options vary between different compilers and its use allows the compiler to include commands that depend on the implementation. In Turbo C compiler directives are #pragma inline and #pragma warn; in Microsoft C are: #pragma pack, #pragma loop_opt and #pragma check_stack.

Exclusive of Turbo C, the #error directive instructs the processor to send a message in case of error in compile time, as in this example:

```
#ifdef MAX
#error Undefined constant.
#endif
```

The program below illustrates the use of some directives of the preprocessor:

# Example-program #10

```
/* Program "Directiv.cpp" */
#include <stdio.h>
#include <assert.h>
#define DEBUG
#define TOP 200

main()
{
#if TOP>100
printf("\n Beginning here.\n");
#else printf("\n Error!");
#endif
assert(TOP<201);
#ifndef DEBUGR
```