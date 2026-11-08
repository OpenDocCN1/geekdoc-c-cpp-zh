exception types may be raised by the functions that you call and, for each, to consider whether you should add a catch block and/or leave it to a calling function to handle the exception. Once you know the exception type, you can usually extract more useful information from the object (like with the `what()` function of our `Trouble` class) and use this for proper error handling and logging. Note also that, especially during development, a program crash is actually better than a catch-all. An at least you learn about potential errors, instead of blindly ignoring them, and can adjust your code to properly prevent them or recover from them.

Make no mistake, we do not mean to say that catch-all blocks should never be used—they certainly have their uses. Catch-all blocks that rethrow after some logging or cleanup, for instance, can be particularly useful. We just want to caution you against using them as an easy, subpar substitute for more targeted error handling.

# Functions That Don’t Throw Exceptions

In principle, any function can throw an exception, including regular functions, member functions, virtual functions, overloaded operators, and even constructors and destructors. So, each time you call a function somewhere, anywhere, you should learn to think about the potential exceptions that might come out and whether you should handle them with a try block. Of course, this does not mean every function call needs to be surrounded by a try block. As long as you are not working in `main()`, it is often perfectly acceptable to delegate the responsibility of catching the exception to the callees of the function.

Sometimes, though, you know full well that the function you are writing won’t ever throw an exception. Some types of functions even should never throw an exception at all. This section briefly discusses these situations and the language facilities that C++ provides for them.

# The noexcept Specifier

By appending the noexcept keyword to the function header, you specify that a function will never throw exceptions. For instance, the following specifies that the doThat() function will never throw:

```
void doThat(int argument) noexcept;
```

If you see a noexcept in a function’s header, you can be sure that this function will never throw an exception. The compiler makes sure that if a noexcept function does unwittingly throw an exception that’s not caught within the function itself, the exception will not be propagated to the calling function at runtime. Instead, the C++ program will treat this as an irrecoverable error and call `std::terminate()`. As discussed earlier in this chapter, `std::terminate()` always results in an abrupt termination of the process.

Note that this does not mean that no exceptions are allowed to be thrown within the function itself; it only means that no exception will ever escape the function. That is, if an exception is thrown during the execution of a noexcept function, it must be caught somewhere within that function and not rethrown. For example, an implementation of doThat() of the following form would be perfectly legal:

```
void doThat(int argument) noexcept
{
    try
    {
        // Code for the function...
    }
}
```