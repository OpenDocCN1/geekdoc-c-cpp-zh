
# Rethrow Exceptions

When a catch catches an exception it may not be able to handle or decide that it is better a higher level to deal with. In this case you can rethink the exception so that it is forwarded to a higher level, relevant with the type of exception, to take over its handling. This is what we just wrote `throw`, without any argument. The throw must be within a catch block or within a function called (directly or indirectly in a call chain) from a catch block. Otherwise the throw causes the program to terminate. The rethrown exception is the original exception that was caught. For example, in the following program, the initial exception of throw is is passed all the way to the catch block that will eventually handle the exception:

```cpp
#include <iostream> // Example 22.5
void f();
void g();

int main() {
    try
    {
        f();
    } catch (int a)
    {
        std::cout << "int exception is caught: " << a << std::endl;
    }
    return 0;
}

void f() {
    try
    {
        g();
    } catch(int indirect) /* Since the catch block does not use the argument I don't use a parameter name. */
    {
        std::cout << "int exception is rethrown\n";
        // Rethrow the exception.
    }
    std::cout << "f() terminates\n"; /* Since throw rethrows the exception, this statement won't be executed. */
}

void g() {
    throw 10;
}
```

The int exception thrown by g() is caught by the catch block in f(). The f() rethrows it and is caught in main(). The original argument of throw is also passed to main(). Therefore, the program displays:

int exception is rethrown
int exception is caught: 10

# 732 Introduction to C++

By the way, this program is also an example of nested try blocks. We also saw in the previous section, a try block, together with its catch blocks, can be nested inside another try block. In this example, the outer block is in main(), while the inner block is in f(). Each try block is associated with its own set of catch blocks, which handles the exceptions that are thrown within it. When an exception is thrown from the inner block, it will be handled by its own catch block. If no blocks match the exception, it will be handled by the catch blocks of the outer try block. If, in f() we change the type in the catch block from int to double, then the exception will be propagated to the outer try block in main(). There, the catch block for type int catches the exception.

In general, as an out parameter, if we change the value of the argument of the exception we can pass a reference to the catch block. For example, let's change the catch block of f():

```cpp
catch(int& b)
{
    b = 20;
    std::cout << "int exception is rethrown\n";
    throw; // Rethrow the exception.
}
```

Now, the value that will be passed to main() when the exception is rethrown is 20.

# Exceptions and Memory Management

When a throw statement is executed, the memory that has been reserved for all the automatic variables in the path between the throw and the catch block that catches the exception is released from the stack. If an automatic variable is object, its destructor is called. For example:

```cpp
#include <iostream> // Example 22.6
#include <cstdlib> // for the exit()

class A
{
private:
    int code;
public:
    A(int c) {code = c};
    ~A() {std::cout << "a" << code << " is destroyed\n";}
};

void f();
void g();

int main() {
    try
    {
        f();
    }
    catch(int)
    {
        std::cout << "int exception is caught\n";
        exit(EXIT_FAILURE); // I just used exit() to remember it.
    }
    std::cout << "Program terminates\n";
    return 0;
}
```

# 22 Exceptions 733

```cpp
void f() {
    A a1(1);
    try {
        g();
    } catch(double) {
        std::cout << "double exception is caught\n";
    }
    std::cout << "f terminates\n";
}
```

```cpp
void g() {
    A a2(2);
    throw 10;
    std::cout << "g terminates\n"; /* I put it there to remember that since the throw is executed, this statement won't be executed. */
}
```

The int exception thrown by g() is forwarded from f() to main(). The memory allocated in the stack with the calls to f() and g() is released. And so it will; since their execution has ended there is no reason for the memory to remain. Thus, the memory for a2 and a1 objects are sequentially released. The exit(1) terminates the program. The program displays:

a2 is destroyed
a1 is destroyed
int exception is caught

What would the program display instead of throw 10; if we write throw double? Now the exception is caught by catch. When it terminates, the destructor of a1 is called. Then the execution continues in main() with the next statement after the catch block. Therefore, the program displays:

a2 is destroyed
double exception is caught
f terminates
Program terminates

With the release of automatic variables, what about the release of dynamically allocated? Take a look at the example below, can you find any problem?

```cpp
void f() {
    int i, *p = new int[10];
    for(i = 0; i < 10; i++) {
        std::cin >> p[i];
        if(p[i] == -1)
            throw 10;
    }
    delete[] p;
}
```

# 734 Introduction to C++

If the exception is thrown, the memory reserved for automatic variables i and p will be released. Notice, however, the memory pointed to by p won't be released. That is, we have a memory leak. One way to solve this is to add delete[] before the throw. That is it is the responsibility of the programmer to release memory has been dynamically allocated before throwing the exception. Another way, which relieves the programmer from this responsibility, is to use smart pointers of the standard library we'll see in Chapter 24. The handling of exceptions in a safe way is to ensure that there will be no memory leaks, that the objects are in a valid state, and that the program will continue to run normally, if that is possible, it is a difficult task, which involves techniques that are outside the scope of this book.

# Standard Exceptions

The standard library provides several classes of exceptions that we can use in our programs. They reside in the std namespace and they are all derived from the exception class. The exception is defined in the exception header. For example, the following program throws such an exception:

```cpp
#include <iostream> // Example 22.7
#include <exception>

void f();

int main() {
    try {
        f();
    } catch (std::exception& e) {
        std::cout << e.what() << '\n';
    }
    return 0;
}

void f() {
    throw std::exception();
}
```

The what() member function is virtual and it returns a string, which is implementation dependent. Its declaration in the exception class looks like:

```cpp
virtual const char* what() const noexcept;
```

If we want to specify the string to be returned, we can override it in a class derived from the exception and throw an exception of that class. For example:

```cpp
class SomeErr : public exception {
public:
    virtual const char *what() const noexcept override {return "Unexpected error\n";}
}
```

```cpp
void f() {
    throw SomeErr();
}
```

As we know, to handle the exception from the derived class we can still use the same catch block with the base reference. If we want to handle them differently, we just add a catch block of the SomeErr type.

The standard library provides many exception types, we only mention some of them. The exception class logic_error and runtime_error classes are derived. These classes, as well as classes derived from them, are defined in the stdexcept file. From the logic_error class the domain_error, invalid_argument, length_error, and the out_of_range classes are derived, which deal with logical errors. Briefly, the domain_error is used to indicate the violation of the domain of a function (e.g., attempt to calculate the square root of a negative number), the invalid_argument is used to indicate unexpected arguments, the length_error is used to indicate that there is no enough space and the out_of_range is used to indicate out of range values (e.g., it is thrown if you use a vector object out of bounds index). For example, suppose that we have a Rectangle class. If a wrong dimension fails in the constructor we can throw an out_of_range exception, like this:

```cpp
Rectangle::Rectangle(double w, double h) {
    if (w <= 0 || h <= 0) {
        throw out_of_range("Wrong dimension");
    }
}
```

From the runtime_error class the range_error, overflow_error, and underflow_error classes are derived, which deal with errors related to the value of valid range or the inability to represent values (e.g., due to overflow) in arithmetic calculations. For more information about the exception types consult a standard library reference.
