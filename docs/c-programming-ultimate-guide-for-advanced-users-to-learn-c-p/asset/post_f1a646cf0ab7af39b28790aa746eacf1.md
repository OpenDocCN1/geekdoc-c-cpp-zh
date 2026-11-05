
It is called. Imagine a scenario in which you have to return at least two pieces of data? For instance, imagine a scenario in which you need to make a method that processes the area of a rectangular shape and furthermore decides whether that rectangular shape is a square? To do this necessitates two pieces of data be returned: the area and a value demonstrating square-ness. This method can't be written using just a single return value. The out modifier takes care of this issue.

In many programming languages, the return of dynamically allocated memory is handled manually. For instance, in C++, you use the delete operator to free memory that was allocated. In any case, C# uses a different, more trouble free approach: garbage collection. C#'s garbage collection system recovers objects automatically—happening directly, off camera, with no programmer intervention. It works this way: When no references to an object exist, that object is thought to be no longer required, and the memory involved by the object is released. This reused memory would then be able to be used for a subsequent allocation.

Garbage collection happens just sporadically during the execution of your program. It will not happen simply in light of the fact that at least one objects exist that are no longer used. In this way, you can't know exactly when garbage collection will occur. It is possible to define a method that will be called only preceding an object's last destruction by the garbage collector. This method is known as a destructor, and it may be used in some very particular circumstances to guarantee that an object ends neatly. For instance, you may use a destructor to guarantee that a system resource claimed by an object is released. It must be expressed at the start that destructors are a very advanced feature that are appropriate to certain specific circumstances. They are not ordinarily required. Be that as it may, in light of the fact that they are a part of C#, they are quickly portrayed here for completion.

In the former example, a parameterless constructor was used. While this is fine for a few circumstances, regularly, you will require a constructor that accepts at least one parameters. Parameters are added to a constructor similarly that they are added to a method: Just announce them inside the brackets after the constructor's name. Since you find out about classes and their constructors, let's investigate the new operator. It has this general structure:

```
`new class-name(arg-list)`
```

Here, class-name is the name of the class that is being instantiated. The class name followed by brackets determines the constructor for the class, as portrayed by the former section. On the off chance that a class doesn't define its own constructor, new will use the default constructor provided by C#. Since memory is limited, it is possible that new won't be able to allocate memory for an object on the grounds that insufficient memory exists. In the event that this occurs, a runtime exception will happen. For the example programs in this book, you won't have to worry about running out of memory, however you should consider this possibility in real projects that you write.

In C#, a variable of a value type contains its own value. Memory to hold this value is automatically given when the program is run. Along these lines, there is no need to explicitly allocate this memory using new. On the other hand, a reference variable stores a reference to an object. The memory to hold this object is allocated dynamically during execution. Not making the primitive types, for example, int or float, into reference types enormously improves the performance of your program. When using a reference type, there is a layer of indirection that adds overhead to each object access. This overhead is avoided by a value type.

## Out Parameter:

Sometimes you will need to use a reference parameter to get a value from a method however not pass in a value. For instance, you may have a method that performs some function, such as opening a network socket, that returns a success/fail code in a reference parameter. In this case, there is no data to pass into the method, yet there is data to pass out. The issue with this situation is that a ref parameter must be initialized to a value before the call. Along these lines, to use a ref parameter would require giving the argument a spurious value just to fulfill this imperative. Luckily, C# gives a better alternative: the out parameter. An out parameter is like a ref parameter with this one special case: It must be used to pass a value out of a method. It isn't necessary (or helpful) to give the variable used as an out parameter an initial value preceding calling the method. The method will give the variable a value. Moreover, inside the method, an out parameter is always considered unassigned; that is, it is expected to have no initial value. Rather, the method must assign the parameter a value before the method's end. In this manner, after the call to the method, the variable referred to by an out parameter will contain a value.

Here is an example that uses an out parameter. The method RectInfo() returns the area of a rectangular shape given the lengths of its sides. In the parameter isSquare, it returns true if the rectangular shape is a square and false otherwise. Consequently, RectInfo() returns two pieces of data to the caller.

When you make a method, you generally know ahead of time the number of arguments that you will pass it, however this isn't always the situation. Sometimes you will need to make a method that can be passed an arbitrary number of arguments. For instance, consider a method that finds the smallest of a set of values. Such a method may be passed as few as two values, or three, or four, etc. In all cases, you need that method to return the smallest value. Such a method can't be made using ordinary parameters. Rather, you should use a special sort of parameter that represents an arbitrary number of parameters. This is done by making a params parameter.

The params modifier is used to declare an array parameter that will be able to get at least zero arguments. The number of elements in the array will be equal to the number of arguments passed to the method. Your program then accesses the array to get the arguments. Each time MinVal() is called, the arguments are passed to it via the nums array. The length of the array approaches the number of elements. Along these lines, you can use MinVal() to find the minimum of any number of values.

Although you can pass a params parameter any number of arguments, they all must be of a type compatible with the array type indicated by the parameter. For instance, calling MinVal() like this:

```
min = ob.MinVal(1, 2.2);
```

is illegal because there is no implicit conversion from double (2.2) to int, which is the type of nums in MinVal().

When using params, you should be careful about limit conditions because a params parameter can accept any number of arguments—even zero! For instance, it is grammatically valid to call MinVal() as shown here:

```
min = ob.MinVal();/no arguments
```

```
min = ob.MinVal(3);/1 argument
```

This is the reason there is a check in MinVal() to confirm that at least one element is in the nums array before there is an attempt to access that element. If the check was not there, a runtime exception would result if MinVal() were called without any arguments. (Later in this book, when exceptions are discussed, you will see a better method to handle these kinds of mistakes.)

Moreover, the code in MinVal() was written so as to allow calling MinVal() with one argument. In that circumstance, the single argument is returned.
