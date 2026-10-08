these pieces being truly independent. When you change a global variable that is used by some other bit of code you are unaware of, you may accidentally break that code.

# Danger!

In Chapter 20 we will learn how to write code which can execute more than one function simultaneously. This is called multi-threaded code. If you use global variables in multi-threaded code you can have a situation where two bits of code are trying to change the same variables at the same time. This is called a *race condition*. To prevent this happening, you need to use a technique called locking. See Chapter 20 for details on how to do this.

# 3.9 Namespaces

We wrote a function called **average** in the previous section. In some ways this isn’t a very good idea because the word average is ambiguous. Do we mean the mean, mode, or median?

This might not seem a big problem. Now we’ve noticed the ambiguity, we could just rename the function.

However, suppose we are using two libraries written by other teams (or perhaps completely different companies). In one library they have used the word **average** to indicate the **mean**. In another library they use the word **average** to indicate the **median**. These functions are not written by us, so we can’t change them. Will this mean the libraries are incompatible?

Furthermore, changing the name of a function isn’t always as easy as it sounds. If we have written a library that somebody else is using, we can’t change the name of a function without also changing their code. For this reason, you can’t normally rename the functions in a library once you have released the library to your customers.

The same problem will occur if two libraries use identically named global variables.

To get round these problems, C++ has a mechanism called *namespaces*. All global variables and functions have an associated namespace which can be used to identify the function more precisely when necessary. Unless you specify the namespace for your functions, they will be put in the *global namespace*.

In a similar way, English people have a first name that you can use to refer to them and a second name that you can use to help resolve ambiguities.