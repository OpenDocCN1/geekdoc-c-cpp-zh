
In this case, a `vector<>` is probably the most appropriate choice. After all, a `vector<>` is specifically designed to manage and manipulate dynamic arrays. Whichever you prefer, the main message of this section remains as follows:

> **Tip** All dynamic memory should be managed by an RAII object. The Standard Library offers both smart pointers (such as `std::unique_ptr` and `std::shared_ptr`) and dynamic containers (such as `std::vector<>`) for this purpose. In the case of smart pointers, `make_unique()` and `make_shared()` should always be used instead of `new` / `new[]` as well. One important consequence of these guidelines is that the `new`, `new[]`, `delete`, and `delete[]` operators generally have no place in a modern C++ program. Be safe: always use an RAII object!

## Standard Library Exceptions

Quite a few exception types are defined in the Standard Library. They’re all derived from the `std::exception` class that is defined in the `<exception>` module, and they all reside in the `std` namespace. For reference, the hierarchy of the standard exception classes is shown in Figure 16-8.

![](img/020c376b6cc4874983a4344f51a256de_614_0.png)

*Figure 16-8.* Standard exception class types and the modules in which they are defined

Many of the standard exception types fall into two groups, with each group identified by a base class that is derived from `exception`. Both these base classes, `logic_error` and `runtime_error`, are defined in the `<stdexcept>` module. For the most part, Standard Library functions do not throw `logic_error` or `runtime_error` objects directly, only objects of types derived from these. The exceptions that derive from them are listed in the first two columns of Figure 16-8. The rules for categorizing types in either branch of the exception hierarchy are as follows:

- The types that have `logic_error` as a base are exceptions thrown for errors that could (at least in principle) have been detected before the program executed because they are caused by defects in the program logic. Typical situations in which `logic_error`s are thrown include calling a function with one or more invalid arguments or calling a member function on an object whose state doesn’t meet the requirements (or preconditions) for that particular function. You can avoid these types of errors in your program by explicitly checking the validity of the arguments or the object’s state prior to the function call.

- The other group, derived from `runtime_error`, is for errors that are generally data dependent and can only be detected at runtime. Exceptions derived from `system_error`, for instance, generally encapsulate errors originating from calls onto the underlying operating system, such as failing file input or output. File access, as any interaction with hardware, can always fail in ways that cannot a priori be predicted (think disk failures, unplugged cables, network failures, and so on).

There are a lot of exception types in Figure 16-8 and we are not going to grind through where they all originate. Your library documentation will identify when a function throws an exception. We only mention some exception types here that are thrown by the operations that you’re already familiar with:

- The `std::out_of_range` exception type is used when accessing array-like data structures with an invalid index (usually defined as lying outside the valid range `[0, size−1]`). Various member functions of `std::string` throw this exception, as do the `at()` accessor functions of, for instance, `std::vector<>` and `std::array<>`. For the latter, the corresponding overloaded operator—the array accessor operator `[]`—does not perform bounds checking on the index. Passing an invalid index to these operators leads to undefined behavior.

- `std::format()` throws a `std::format_error` when passed an invalid format string. To debug why a new format string is failing, it can therefore be useful to temporarily surround the corresponding `std::format()` expression with a try-catch block and to print out the result of invoking `what()` on the caught exception (see also Chapter 2). Once the format string works, though, `std::format()` will normally never throw again, and you should remove this debugging code again. It would only clutter your code otherwise.

- The `typeid()` operator throws a `std::bad_typeid` exception if applied on a dereferenced null pointer to a polymorphic type.

- A `std::bad_cast` exception is thrown by a `dynamic_cast<T&>(expr)` operation if `expr` cannot be cast to `T&`. An exception can occur only when casting to a reference type `T&`. When failing to cast to a pointer type `T*`, `dynamic_cast<T*>(expr)` simply evaluates to `nullptr` instead.

- Calling the `value()` member of a `std::optional<>` object that doesn’t hold a value will throw a `bad_optional_access` exception. The `*` and `->` operators of `optional<>` never throw exceptions, though. Using these on an `optional<>` without a value results in undefined behavior. In practice, this means you will read junk data.

- A `std::bad_alloc` exception (or another exception derived from `bad_alloc`) may be thrown by operators `new` and `new[]`. Operator `new[]`, for instance, throws a `std::bad_array_new_length` exception if it’s passed a negative or excessively large array size. But even with valid inputs, either operator may throw a `bad_alloc` exception if memory allocation fails. Possible causes are corruption of the free store, or a lack of available memory. And by extension any operation that requires dynamic memory allocation may throw `bad_alloc` exceptions as well. Notable examples of such operations include, for instance, copying or adding elements to `std::vector<>` or `std::string` objects.

## The Exception Class Definitions

You can use a standard exception class as a base class for your own exception class. Since all the standard exception classes have `std::exception` as a base, it’s a good idea to understand what members this class has because they are inherited by all the other exception classes. The exception class is defined in the `<exception>` module like this:

```cpp
namespace std
{
  class exception
  {
  public:
    exception() noexcept;                         // Default constructor
    exception(const exception&) noexcept;         // Copy constructor
    exception& operator=(const exception&) noexcept; // Assignment operator
    virtual ~exception();                         // Destructor
    virtual const char* what() const noexcept;    // Return a message string
  };
}
```

This is the public class interface specification. A particular implementation may have additional non-public members. This is true of the other standard exception classes too. The noexcept keyword that appears in the declaration of the member functions specifies that they do not throw exceptions, as we discussed earlier. The destructor is noexcept by default. Notice that there are no member variables. The null-terminated string returned by `what()` is defined within the body of the function definition and is implementation dependent. This function is declared as virtual, so it will be virtual in any class derived from `exception`. If you have a virtual function that can deliver a message that corresponds to each exception type, you can use it to provide a basic, economical way to record any exception that’s thrown.

A catch block with a base class parameter matches any derived class exception type, so you can catch any of the standard exceptions by using a parameter of type `exception`. Of course, you can also use a parameter of type `logic_error` or `runtime_error` to catch any exceptions of types that are derived from these. You could provide the `main()` function with a try block, plus a catch block for exceptions of type `exception`:

```cpp
int main()
{
  try
  {
    // Code for main...
  }
}
```
