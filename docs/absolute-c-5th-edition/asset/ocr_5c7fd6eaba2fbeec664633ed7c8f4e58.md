# Exception Handling Basics 845

```
void someFunction() throw ( );
//Empty exception list, so all exceptions invoke unexpected().
```

```
void someFunction();
//All exceptions of all types are treated normally.
```

The default action of unexpected() is to end the program. You need not use any special include or using directives to gain the default behavior of unexpected(). You have no need to redefine the behavior of unexpected(); it can be changed by the function set_unexpected(). If you need to use set_unexpected(), you should consider a more advanced book for the details.

If D is a derived class of class B and B is in the exception specification, then an object of class D will be treated normally, it is an object of class B. However, automatic type conversions are not allowed. If double is in the exception specification, this does not account for throwing an int value. You need to include both int and double in the exception specification.

One final warning: Not all compilers treat the exception specification as they are supposed to. With compilers, the exception specification has no effect on your code. This is another reason to place all exceptions that might be thrown by your functions in the throw specification. This way all compilers will treat your exceptions in the same manner. Of course, you could get the same compiler consistency by not having any throw specification at all, but then your program would not be as well documented and you would not get the extra error checking provided by compilers that do use the throw specification. With a compiler that does process the throw specification, your program will terminate as soon as it throws an exception that you did not anticipate. (Note that this is a run-time behavior—but which run-time behavior you depends on your compiler).

Warning!

# PITFALL: Exception Specification in Derived Classes

![](bbox=[0.105, 0.656, 0.183, 0.693])

When you redefine or override a function definition in a derived class, it should have the same exception specification as it had in the base class, or it should have an exception specification whose exceptions are subset of those in the base class specification. Put another way, when you redefine or override a function definition, you cannot add any exceptions to the exception specification (but you can delete some exceptions if you want). This makes sense, since an object of the derived class can be used anywhere an object of the base class can be used, and so a redefined or overwritten function must fit any code written for an object of the base class.