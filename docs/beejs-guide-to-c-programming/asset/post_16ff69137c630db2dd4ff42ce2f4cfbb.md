
# Chapter 5

## Pointers—Cower In Fear!

"How do you get to Carnegie Hall?"
"Practice!"

—20th-century joke of unknown origin

Pointers are one of the most feared things in the C language. In fact, they are the one thing that makes language challenging at all. But why?

Because, quite honestly, can cause electric shocks to come up through the keyboard and physically weld your arms permanently in place, cursing you to a life at the keyboard from the 70s!

Really? Well, not really. I'm trying to set you up for success.

Depending on what language you came from, you might already understand the concept of references, where a variable refers to an object of some type.

This is very much the same, we have to be more explicit with C about when we're talking about the reference or what it refers to.

## 5.1 Memory and Variables

Computer memory holds data of all kinds, right? It'll hold floats, ints, or whatever you have. To make memory easy to copy, each byte of memory is identified by an integer. These integers increase sequentially as you move through memory. You can think of it as a bunch of numbered boxes, where each box holds a byte of data. Or a big array where each element holds a byte, if you come from a language with arrays. The number that represents each box is called its address.

Now, not all data types use a byte. For instance, int is often four bytes, as a float is, but it really depends on the system. You can use the sizeof operator to determine how many bytes of a certain type use.

```
// zu is the format specifier for size_t
```

```
printf("int uses %zu bytes of memory\n", sizeof(int));
```

```
// That prints "4" for me, but can vary by system.
```

> Typically. I'm sure there are exceptions out there in the dark corridors of computing history.
A byte is made up of no more than 8 binary digits, or bits for short. This means in decimal digits just like grandma used to use, it can hold an unsigned number between 0 and 255, inclusive.

**Memory Fun Facts:** When you have a data type (like your typical int) that uses more than a byte of memory, the bytes that make up the data are always adjacent to one another in memory. Sometimes they're in the order that you expect, and sometimes they're not. While C doesn't guarantee any memory order (it's platform-dependent), it's still possible to write code in a way that's platform-independent where you don't have to consider these pesky order.

So anyway, if we can get on it and get a drum roll and some foreoding magic for the definition of a pointer, a pointer is a variable that holds an address. Imagine the classic story from 2001: A Space Odyssey at this point. Bam ba bam bam BAAAH!

Ok, so might be a bit overwhelmed, there's not a lot of mystery about pointers. They are the address of data. Just like an int can hold the value 12, a pointer variable can hold the address of data.

This means all these things mean the same thing, i.e. a number that represents a pointer in memory:

- Index into memory (if you're thinking of memory like a big array)
- Address
- Location

I'm going to use these interchangeably. And I just threw location there because you can never have enough that mean the same thing.

And a pointer variable holds address number. Just like a float variable might hold 3.14159.

Imagine you have a bunch of Post-it® all numbered in sequence with their addresses. The first one is int 0, the next is index 1, and so on.

In addition to the number representing their positions, you can also write another number of choice on each. It could be the number of days you have or the months around Mars...

...Or, it could be the index of another pointer-note!

If you have written the number of data you have, that's a regular variable. But if you write the index of another-Post-it in there, that's a pointer. It points to the other note!

Another analogy might be with addresses. You can have a house with certain qualities, metal roof, solar, etc. You or to have the address of that house. The address isn't the same as the house itself. One's a full-blown house, and the other is just a few lines of text. But the address of the house is a pointer to find where it is. It isn't the house, but it tells you where to find it.

And we can do this in the computer with data. You can have a data variable that holds some value. And value is in memory at some address. And you could have a different pointer variable hold the address of that variable.

It's not the data variable itself, but like a "pointer" to data. It tells us where to find it.

When we have, we say we have a "pointer" to data. And we can follow the pointer to access the data itself.

(Though doesn't seem particularly useful, this becomes indispensable when used with function calls. Bear with me we got there.)

So if we have an int, and we want a pointer to it, what is some way to get the address of that int, right? After all, the pointer holds the address of data. What operator do you suppose we'd use to find the address of the int?

Well, a shocking surprise that comes as something of a shock to you, gentle reader, we use the address operator (which happens to be an ampersand: "&") to find the address of the data. Ampersand.

> The order that bytes come in is referred to as endianness of the number. The usual suspects are big-endian (with the most significant byte first) and little-endian (with the most-significant byte last), or commonly now, mixed-endian (with the most-significant byte somewhere else).

For a quick example, we'll introduce a new format specifier for printf() you can print a pointer. We know how %d prints a decimal integer? Well, %p prints a pointer. Now, this pointer is going to look like a garbage number (and it might be printed in hexadecimal instead of decimal), but it is merely the index into memory where data is stored. (Or the index into the memory that the first byte of data is stored in, if the data is multi-byte). In virtually all circumstances, including this, the actual value of the number printed is unimportant to you, and I show it here only for demonstration of the address-of operator.

```
#include <stdio.h>

int main(void)
{
    int i = 10;

    printf("The value of i is %d\n", i);
    printf("And its address is %p\n", (void *)&i);

    // %p expects the argument to be a pointer to void
    // so we cast it to make the compiler happy.
}
```

On my computer, this prints:
The value of i is 10
And its address is 0x7ffd7072a4

If you're curious, that hexadecimal is 140,727,326,896 in decimal (base 10 like Grandma used to use). It's the index into memory where the variable i is stored. It's the address of i. It's the location of i. It's a pointer to.

It's a pointer because it knows where i is in memory. Like a home address written on scrap of paper tells you you can find a particular house, this number indicates where in memory we can find the value of i. It points to i.

Again, we don't really care what the's exact number is, Generally we just care that it's a pointer to i.

## 5.2 Pointer Types

So this is well and good. You can now successfully address the address of a variable and print it on the screen. It's a little something for the ol' resume, right? Here's where you grab me by the scuff of the neck and ask quite what the fricker pointers are good for.

Excellent question, and we'll get to that after these messages from our sponsor.

ACME ROBOTIC HOUSING UNIT CLEANING SERVICES. YOUR HOMESTAD WILL BE DRAMALLY IMPROVED OR WILL BE TERMINATED. MESSAGE ENDS.

Welcome back to another installment of Beej's Guide. When we met last we were talking about how to use of pointers. Well, what we're going to do is store a pointer in a variable so we can use it later. You can identify the pointer type there's an asterisk (*) before the variable name and after its type:

```
int main(void)
{
    int i; // i's type is "int"
    int p; // p's type is "pointer to an int", or "int-pointer"
}
```

> *That is, base 16 with digits 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, and F.
