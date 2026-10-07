ClassB's declaration and definition remain unchanged. Let's try compiling and running this program again.

# Program 8.7 Output

| x | 100 |
| x | 200 |

Now we can talk about the actual example. First, a and b are defined to be ClassA and ClassB object, respectively. After allocation and initialization, a message is sent to a asking to apply the initVar method. This method is defined in the definition of ClassA, so this method is selected simply sets the value of the instance variable to 100 and returns. The printVar method, which you just added to ClassA, is invoked next to display the value of x.

As with the ClassA object, the ClassB object b is allocated and initialized, its instance variable x is set to 200, and finally its value displayed.

Be sure you understand how the proper method is chosen for a and b based on which class they belong to. This is a fundamental concept of object-oriented programming in Objective-C.

As an exercise, consider removing the printVar method from ClassB. Would this work? Why or why not?

# Overriding the dealloc Method and the Keyword super

Now that you know how to override methods, let's return to Program 8.5B to learn a better approach to releasing the memory occupied by the origin. The setOrigin method allocates its own XPoint origin object, and you are responsible for releasing its memory. The approach used in Program 8.6 was to make release that memory with a statement such as follows:

```
[myRect origin]
```

You don't have to worry about releasing all the individual members of a class; you can override the inherited dealloc method (it's inherited from NSObject) and release the origin's memory there.

# Note

> Don't override the release method—you override dealloc instead. As you will learn in a later chapter, release sometimes gives up the memory an object used, and sometimes it doesn't. It gives up the memory taken by an object only if no else is referencing that object. And not by this invoking the object's dealloc method, the method that actually gets called by the system when the object is to be destroyed.