# Is it possible to nest try-catch blocks?

![](bbox=[0.141, 0.173, 0.183, 0.201])

Yes, you can nest one try-catch block inside another. Given below is the syntax of nesting of try-catch blocks. If there is any exception in the statements written in the inner try block, C++ will first check if there is a catch corresponding to the try in which the exception occurred. If yes, the respective catch block will be executed.

If there is no catch block corresponding to an inner try block for this type of exception, C++ will check all catch blocks corresponding to the outer try block to find the best matching handler for the exception. If there is an outer catch block corresponding to this exception, it will be executed and the exception will be considered as handled. If there is no matching catch block found for an exception, then the exception will be considered as unhandled and the program will crash. The aim of the exception handling is to avoid program crashes abruptly, and hence it is recommended to handle all the possible exceptions some way or the other to make the program robust.

For instance, if an exception of Type 3 occurs in the inner try block, the catch block written corresponding to the outer try block that handles exception of Type 3 will get executed, and the exception will be considered as handled. If exception of Type 1 or Type 2 is generated in the inner try block, the respective inner catch block will be executed and the exception will be considered as handled by the inner try-catch blocks itself. Remember that if there is an exception generated in the statements of the outer try block, then C++ will not handle them using the inner catch blocks.

```
try
{
/*statements in outer try block*/
    try
    {
    /*statements in inner try block*/
    }
    catch(Type1 obj1)
    {
    /*To handle exceptions of Type 1 in the inner try block*/
    }
    catch(Type2 obj2)
    {
    /*To handle exceptions of Type 2 in the inner try block*/
    }
    …… (many inner catch blocks possible)
}
/*some more statements in outer try block*/
catch(Type3 obj3)
{
/*To handle exceptions of Type 3 in the inner and outer try block*/
}
catch(Type4 obj4)
{
/*To handle exceptions of Type 4 in the inner and outer try block*/
}
…… (many outer catch blocks possible)
```

# 17.6  Catching and Throwing User-defined Objects

Just like we can throw and catch primitive data items, we can also throw user-defined objects. As an example, let us go back to the Account class created in Chapter 11, Section 11.7 for managing bank accounts. We will modify the same code to use exception handling.