```
{
    cout << "Send for help.\n";
}
```

With this second ordering, an exception (a thrown value) of type NegativeNumber will be caught by the NegativeNumber catch block, as it should be. However, if a value of type DivideByZero were thrown, it would be caught by the block that starts catch(...). So, the DivideByZero catch block could never be reached. Fortunately, most compilers tell you if you make this sort of mistake.

# PROGRAMMING TIP Exception Classes Can Be Trivial

Here we reproduce the definition of the exception class DivideByZero from Display 16.4:

```
class DivideByZero
{};
```

This exception class has no member variables and no member functions (other than the default constructor). It has nothing but its name, but that is useful enough. Throwing an object of the class DivideByZero can activate the appropriate catch block, as it does in Display 16.4.

When using a trivial exception class, you normally do not have anything you can do with the exception (the thrown value) once it gets to the catch block. The exception is just being used to get you to the catch block. Thus, you can omit the catch-block parameter. (You can omit the catch-block parameter anytime you do not need it, whether the exception type is trivial or not.)

# Throwing an Exception in a Function

Sometimes it makes sense to delay handling an exception. For example, you might have a function with code that throws an exception if there is an attempt to divide by zero, but you may not want to catch the exception in that function. Perhaps some programs that use that function should simply end if the exception is thrown, and other programs that use the function should do something else. So you would not know what to do with the exception if you caught it inside the function. In these cases, it makes sense to not catch the exception in the function definition, but instead to have any program (or other code) that uses the function place the function invocation in a try block and catch the exception in a catch block that follows that try block.

Look at the program in Display 16.5. It has a try block, but there is no throw statement visible in the try block. The statement that does the throwing in that program is

```
if (bottom == 0)
    throw DivideByZero();
```