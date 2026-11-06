
```cpp
{
    cin.exceptions(ios::failbit);   // throw exception on fail
    while (true)
    {
        try
        {
            cout << "enter a number: ";
            int value;
            cin >> value;
            cout << "you entered " << value << '\n';
        }
        catch (ios::failure const &problem)
        {
            cout << problem.what() << '\n';
            cin.clear();
            cin.ignore(INT_MAX, '\n'); // ignore the faulty line
        }
    }
}
```

By default, exceptions raised from within `ostream` objects are caught by these objects, which set their `ios::badbit` as a result. See also the paragraph on this issue in section 14.8.

## 10.8 Standard Exceptions

All data types may be thrown as exceptions. Several additional exception classes are now defined by the C++ standard. Before using those additional exception classes the `<stdexcept>` header file must have been included. All of these *standard exceptions* are class types by themselves, but also offer all facilities of the `std::exception` class. Objects of the standard exception classes may also be considered objects of the `std::exception` class.

The `std::exception` class offers the member

```cpp
char const *what() const;
```

describing in a short textual message the nature of the exception.

C++ defines the following standard exception classes:

- `std::bad_alloc` (this requires the `<new>` header file): thrown when `operator new` fails;
- `std::bad_exception` (this requires the `<exception>` header file): thrown when a function tries to generate another type of exception than declared in its function throw list;
- `std::bad_cast` (this requires the `<typeinfo>` header file): thrown in the context of *polymorphism* (see section 14.6.1);
- `std::bad_typeid` (this requires the `<typeinfo>` header file): also thrown in the context of *polymorphism* (see section 14.6.2);

All additional exception classes were derived from `std::exception`. The constructors of all these additional classes accept `std::string const &` arguments summarizing the reason for the exception (retrieved by the `exception::what` member). The additionally defined exception classes are:

- `std::domain_error`: a (mathematical) domain error is detected;
- `std::invalid_argument`: the argument of a function has an invalid value;
- `std::length_error`: thrown when an object would have exceeded its maximum permitted length;
- `std::logic_error`: a logic error should be thrown when a problem is detected in the internal logic of the program. Example: a function like C’s `printf` is called with more arguments than there are format specifiers in its format string;
- `std::out_of_range`: thrown when an argument exceeds its permitted range. Example: thrown by `at` members when their arguments exceed the range of admissible index values;
- `std::overflow_error`: an overflow error should be thrown when an arithmetic overflow is detected. Example: dividing a value by a very small value;
- `std::range_error`: a range error should be thrown when an internal computation results in a value exceeding a permissible range;
- `std::runtime_error`: a runtime error should be thrown when a problem is encountered that can only be detected while the program is being executed. Example: a non-integral value is entered when the program’s input expects an integral value.
- `std::underflow_error`: an underflow error should be thrown when an arithmetic underflow is detected. Example: dividing a very small value by a very large value.

## 10.9 Exception guarantees

Software should be *exception safe*: the program should continue to work according to its specifications in the face of exceptions. It is not always easy to realize exception safety. In this section some guidelines and terminology is introduced when discussing exception safety.

Since exceptions may be generated from within all C++ functions, exceptions may be generated in many situations. Not all of these situations are immediately and intuitively recognized as situations where exceptions can be thrown. Consider the following function and ask yourself at which points exceptions may be thrown:

```cpp
void fun()
{
    X x;
    cout << x;
    X *xp = new X(x);
    cout << (x + *xp);
    delete xp;
}
```

If it can be assumed that `cout` as used above does not throw an exception, there are at least 13 opportunities for exceptions to be thrown:

- `X x`: the default constructor could throw an exception (#1)
- `cout << x`: the overloaded insertion operator could throw an exception (#2), but its rvalue argument might not be an X but, e.g., an `int`, and so `X::operator int() const` could be called which offers yet another opportunity for an exception (#3).
- `*xp = new X(x)`: the copy constructor may throw an exception (#4) and operator new (#5a) too. But did you realize that this latter exception might not be thrown from `::new`, but from, e.g., X’s own overload of `operator new`? (#5b)
- `cout << (x + *xp)`: we might be seduced into thinking that two X objects are added. But it doesn’t have to be that way. A separate class Y might exist and X may have a conversion operator `operator Y() const`, and `operator+(Y const &lhs, X const &rhs), operator+(X const &lhs, Y const &rhs), and operator+(X const &lhs, X const &rhs)` might all exist. So, if the conversion operator exists, then depending on the kind of overload of operator+ that is defined either the addition’s left-hand side operand (#6), right-hand side operand (#7), or operator+ itself (#8) may throw an exception. The resulting value may again be of any type and so the overloaded cout << return-type-of-operator+ operator may throw an exception (#9). Since operator+ returns a temporary object it is destroyed shortly after its use. X’s destructor could throw an exception (#10).
- `delete xp`: whenever operator new is overloaded, operator delete should be overloaded as well and may throw an exception (#11). And of course, X’s destructor might again throw an exception (#12).
- `}`: when the function terminates the local x object is destroyed: again an exception could be thrown (#13).

It is stressed here (and further discussed in section 10.11) that although it is possible for exceptions to leave destructors, this would violate the C++ standard and so it must be prevented in well-behaving C++ programs.

How can we expect to create working programs when exceptions might be thrown at this many situations?

Exceptions may be generated in a great many situations, but serious problems are prevented when we’re able to provide at least one of the following exception guarantees:

- The *basic guarantee*: no resources are leaked. In practice this means: all allocated memory is properly returned when exceptions are thrown.
- The *strong guarantee*: the program’s state remains unaltered when an exception is thrown (as an example: the canonical form of the overloaded assignment operator provides this guarantee).
- The *nothrow guarantee*: this applies to code for which it can be proven that no exception can be thrown from it.

### 10.9.1 The basic guarantee

The *basic guarantee* dictates that functions that fail to complete their assigned tasks must return all allocated resources, usually memory, before terminating. Since practically all functions and operators may throw exceptions and since a function may repeatedly allocate resources the blueprint of a function allocating resources shown below defines a try block to catch all exceptions that might be thrown. The catch handler’s task is to return all allocated resources and then rethrow the exception.

```cpp
void allocator(X **xDest, Y **yDest)
{
    X *xp = 0;                 // non-throwing preamble
    Y *yp = 0;

    try                         // this part might throw
    {
        xp = new X[nX];         // alternatively: allocate one object
        yp = new Y[nY];
    }
    catch(...)
    {
        delete[] xp;
        throw;
    }

    delete[] *xDest;            // non-throwing postamble
```
