# 22 • Exceptions 725

C++11 introduces the noexcept operator. It is a unary operator, which returns true or false if its operand may throw an exception or not. Like sizeof, noexcept does not evaluate the operand. For example:

```
noexcept(f(i&)) /* Since f() is declared not to create exceptions
operator returns true. */
void h();
noexcept(h()) /* Since h() is not declared to create the exceptions
operator returns false. */
```

The return value of the noexcept operator can be used as an argument in order to declare whether a function may throw or not. For example:

```
void a() noexcept(noexcept(b())) /* If b does not create exceptions,
neither does a(). If b() may create exceptions, a() may also create
exceptions. */
```

# Discussing about Exceptions

Now that you have an idea about the exceptions, let's have a brief discussion about how useful they might be. One might ask why not use the traditional technique, that is, to make the function return values that correspond to errors and let the caller check the return value and handle the errors? Of course we could do that, but it is not always possible. The integer values that a function returns may be valid and not for error coding. Even if it is possible, these checks must be done after each function call, which being a tedious task, it may significantly increase the size of the program. By placing the function in a try block, the catch Blocks will differ only once.

Sometimes we cannot return a value. For example, when we create an object, if an error occurs in the constructor of the class there is no return value to return. How can we handle it? Someone might answer that, we could define a private variable in the class with a public value. If its, for example, is 0, it means that the construction of the object was successful; otherwise, its value indicates the error. Instead of doing all this, it is simpler for the constructor to throw an exception and inform us about the failure. If it throws, the catch block will handle it themselves, otherwise memory leaks and unpredictable behavior of the program may occur.

In some situations the error has been transmitted up a function chain to the general caller. If an error occurs in a nested function (e.g., a() calls b() which calls c()), then d() and the error occurs in d(), we can throw an exception and inform us which function made the first call (e.g., a()) The traditional approach to return values from each function to its immediate caller all the way up to the first one (e., a()) requires more code and makes the program more complex, inflexible, and inefficient, prone since the programmer may forget to forward some return value.

On the other hand, it is not clear, I would recommend using exceptions. Separating detection from handling simplifies and makes the program more readable, but this is a general rule, it does not necessarily apply in all cases. It's not black or white, that is, never use return codes or never exceptions.

Each program has its own requirements. For example, if the program user input, and wrong data are entered, this is not a serious problem to throw an exception. The program can simply discard the input and prompt the user to enter new data. In this case, the code that handles the wrong input combined with the code that handles the overall data input process. After all, the choice of the name exception implies that it is used to signal exceptional errors and not trivial errors. In another example,