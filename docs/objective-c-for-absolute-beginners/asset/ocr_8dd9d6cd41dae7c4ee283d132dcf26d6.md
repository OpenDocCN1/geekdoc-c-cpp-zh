Hopefully, you are getting used to zero-based arrays. Line 9 also makes use of the dereference operator, the asterisk (*); there is more about this in the next section.

Line 10 is equivalent to line 8. Both myArray and aPointer effectively point to the memory, so the array operator works.

# Using the Dereference Operator

Line 9 looked a little different from the other lines, let's examine it a little closer:

```
letter = *(aPointer + 2);
```

First, let's consider what's inside the parentheses:

```
aPointer + 2
```

This should be pretty straightforward: we are adding 2 to the pointer aPointer. If aPointer is 0x1000, the resulting value would be 0x1002. The new pointer points to the letter "C". Using this pointer is very different from using the brackets in lines 8 or 10. We manually adjust the pointer so that it results in a value. Next we need to ask the computer, "What does the pointer point to? With the array operator on lines 8 and 10 of List 13-1, question is implied, and the program responds. When we simply change an address by adding, subtracting, and so on, the program needs to explicitly ask this question. Here is where the asterisk (*) comes into play.

Using an asterisk in front of a pointer dereferences the address and returns what value the pointer is pointing to. So, if our pointer is 0x1000, we can get the letter "A" by dereferencing the pointer. *(0x1000) would return the letter "A" if our example was pointing to real memory (don't actually do this because 0x1000 is not a real address, just example is used to simplify the problem). Remember, a pointer is an address and an address is just a number. The asterisk asks the computer to return what's stored at the address rather than to return the address itself.

> NOTE: In most common programming, the program rarely tells the system, for example, at location 0x1000 is our data. The reason for that this memory is virtualized. Virtual memory allows more memory to be used than is physically present on the machine (virtual memory is out of scope of this book). Because of this, the operating system manages where the data is stored. As a result, the computer tells the program where its memory is, rather than the program telling the computer. Regardless, the concept is the same.

When developing software at the hardware or device driver level, using hard-coded addresses is much more common. Typical programs in Mac OS or iOS will never use hard-coded addresses.