# Chapter 30

# Variable-Length Arrays (VLAs)

C provides a way for you to declare an array whose size is determined at runtime. This gives you the benefits of dynamic runtime sizing like you get with malloc(), but without needing to worry about free()ing the memory after.

Now, a lot of people don't like VLAs. They've been banned from the Linux kernel, for example. We'll dig into more of that rationale later.

This is an optional feature of the language. The macro __STC_NO_VLA__ is set to 1 if VLAs are not present (They were mandatory in C99, and then become optional in C11).

```
#if __STC_NO_VLA__ == 1
  #error Sorry, need VLAs for this program!
#endif
```

But since neither GCC nor Clang bather to define this macro, you may get limited mileage from this. Let's dive first with an example, and then we'll look for the devil in the details.

# 30.1 The Basics

A normal array is declared with a constant size, like this:

```
int v[10];
```

With VLAs, we can use a size determined at runtime to set the array, like this:

```
int n = 10;
int v[n];
```

Now, that looks like the same thing, and in many ways is, but this gives you the flexibility to compute the size you need, and then get an array of exactly that size.

Let's ask the user to input the size of the array, and then store the index-times-10 in each of those array elements:

```
#include <stdio.h>
```

```
int main(void)
{
  int n;

  printf("Enter a number: "); fflush(stdout);
```