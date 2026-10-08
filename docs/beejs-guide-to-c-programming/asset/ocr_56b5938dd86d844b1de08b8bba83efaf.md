# Chapter 11

# Pointers II: Arithmetic

Time to get to know it with a number of new pointer topics! If you're not up to speed with pointers, check the first section in the guide on the matter.

# 11.1 Pointer Arithmetic

Turns out you can do on pointers, notably addition and subtraction.

But what does it mean when you do that?
In short, if you have a pointer to a type, adding one to the pointer moves to the next item of that type directly after it in memory.

It's important to remember that as we move pointers around and look at different places in memory, we need to make sure that we're always pointing to a valid place in memory before dereference. If we're off in the weeds and we're try to see what's there, the behavior is undefined and a crash is a common result.

This is a little chicken-and-egg with Array/Pointer Equivalence, below, but we're going to give it a shot, anyway.

# 11.1.1 Adding to Pointers

First, let's create an array of numbers.

```
int a[5] = {11, 22, 33, 44, 55};
```

Then let's get a pointer to the first element in that array:

```
int a[5] = (11, 22, 33, 44, 55);
```

```
int *p = &a[0]; // Or "*p = a;" works as well
```

Then let's print the value by dereferencing the pointer:

```
printf("%d\n", p); // Prints 11
```

Now let's use pointer arithmetic to print the next element in the array, one at index 1:

```
printf("%d\n", (p + 1)); // Prints 22!!
```

What happened there? C knows that p is a pointer to an int. So it knows the sizeof of int and knows to skip that many bytes to get the next int after the first one!

> Recall the sizeof operator tells you the size in bytes of an object in memory.