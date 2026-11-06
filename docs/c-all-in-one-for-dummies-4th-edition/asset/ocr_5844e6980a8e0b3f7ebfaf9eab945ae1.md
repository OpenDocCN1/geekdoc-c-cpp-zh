This code calls `new`, but also provides a number in parentheses. That number is put in the memory initially, instead of being assigned to it later. This line of code is equivalent to the following two lines of code:

```
int *ptr = new int;
*ptr = 10;
```

![](bbox=[0.173, 0.221, 0.239, 0.296])

When you initialize a value in the new operator, the technical phrase for what you are doing is *invoking a constructor*. The reason is that the compiler adds a bunch of code to your application — code that operates behind the scenes. This code is the *runtime library*. The library includes a function that initializes an integer variable if you pass an initial value. The function that does this is known as a *constructor*. When you run it, you are *invoking* it. Thus, you are invoking the constructor. For more information on constructors, see Book 2, Chapter 1.

# Freeing Raw Pointers

When you allocate memory on the heap by calling the `new` operator and you’re finished using the memory, you need to let the computer know, regardless of whether it’s just a little bit of memory or a lot. The computer doesn’t look ahead into your code to find out whether you’re still going to use the memory. So in your code, when you are finished with the memory, you *free* the memory.

The way you free the memory is by calling the `delete` operator and passing the name of the pointer:

```
delete MyPointer;
```

This line would appear after you’re finished using a pointer that you allocated by using `new`. (Like the new operator, `delete` is also an operator and does not require parentheses around the parameter.)

The FreePointer example, shown in Listing 8-9, provides a complete demonstration of allocating a pointer, using it, and then freeing it. Note the use of the `replace()` method, which first appears in the “Replacing parts of a string” section of Book 1 Chapter 6. You use the arrow operator (->) to access this string method of phrase. The “Using classes and raw pointers” section of Book 2 Chapter 1 describes the arrow operator in more detail.