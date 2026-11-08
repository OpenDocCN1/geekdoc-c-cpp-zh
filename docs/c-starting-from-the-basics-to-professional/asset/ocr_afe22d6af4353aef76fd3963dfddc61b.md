We can demonstrate the effects of this with a simple example. The following calls a function that attempts to modify one of its arguments, and of course, it fails miserably:

```
```cpp
// Ex8_03.cpp
// Failing to modify the original value of a function argument
import <iostream>;

double changeIt(double value_to_be_changed);    // Function prototype

int main()
{
    double it {5.0};
    double result {changeIt(it)};

    std::cout << "After function execution, it = " << it
              << "\nResult returned is " << result << std::endl;
}

// Function that attempts to modify an argument and return it
double changeIt(double it)
{
    it += 10.0;                    // This modifies the copy
    std::cout << "Within function, it = " << it << std::endl;
    return it;
}
```
```

This example produces the following output:

```
```text
Within function, it = 15
After function execution, it = 5
Result returned is 15
```
```

The output shows that adding 10 to it in the changeIt() function has no effect on the variable it in main(). The it variable in changeIt() is local to the function, and it refers to a copy of whatever argument value is passed when the function is called. Of course, when the value of it that is local to changeIt() is returned, a copy of its current value is made, and it’s this copy that’s returned to the calling program.

Pass-by-value is the default mechanism by which arguments are passed to a function. It provides a lot of security to the calling function by preventing the function from modifying variables that are owned by the calling function. However, sometimes you do want to modify values in the calling function. Is there a way to do this when you need to? Sure there is; one way is to use a pointer.

# Passing a Pointer to a Function

When a function parameter is a pointer type, the pass-by-value mechanism operates just as before. However, a pointer contains the address of another variable; a copy of a pointer contains the same address and therefore points to the same variable.

If you modify the definition of the first changeIt() function to accept an argument of type double*, you can pass the address of it as the argument. Of course, you must also change the code in the body of changeIt() to dereference the pointer parameter. The code is now like this: