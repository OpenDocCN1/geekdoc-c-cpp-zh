
overflow_error underflow_error system_error
bad_array_new_length ios_base::failure

This hierarchy attempts to provide a framework for exceptions beyond the ones defined by the standard library. Logic errors are errors that in principle could be caught either before the program starts executing or by tests of arguments to functions and constructors. Run-time errors are all other errors. The system_error is described in §30.4.3.3.
The standard-library exception hierarchy is rooted in class exception:

```
class exception {
public:
exception();
exception(const exception&);
exception& operator=(const exception&);
virtual ~exception();
virtual const char* what() const;
};
```

The what() function can be used to obtain a string that is supposed to indicate something about the error that caused the exception.
A programmer can define an exception by deriving from a standard-library exception like this:

```
struct My_error : runtime_error {
My_error(int x) :runtime_error{"My_error"}, interesting_value{x} { }
int interesting_value;
};
```

Not all exceptions are part of the standard-library exception hierarchy. However, all exceptions thrown by the standard library are from the exception hierarchy.

Unless you know that no facility is used in a way that could throw an exception, it is a good idea to somewhere catch all exceptions. For example:

```
int main()
try {
// ...
}
catch (My_error& me) { // a My_error happened
// we can use me.interesting_value and me.what() }
catch (runtime_error& re) { // a runtime_error happened
// we can use re.what()
}
catch (exception& e) { // some standard-library exception happened
// we can use e.what()
}
catch (...) { // Some unmentioned exception happened
// we can do local cleanup
}
```

As for function arguments, we use references to avoid slicing (§17.5.1.4).

## 30.4.1.2 Exception Propagation

In <exception>, the standard library provides facilities for making propagation of exceptions accessible to programmers:

Section 30.4.1.2 Exception Propagation 871

# Exception Propagation (§iso.18.8.5)

**exception_ptr** Unspecified type used to point to exceptions

**ep=current_exception() ep** is an **exception_ptr** to the current exception, or to no exception if there is no currently active exception; noexcept

**rethrow_exception(ep)** Re-throw the exception pointed to by **ep**; **ep**’s contained pointer must not be **nullptr**; noreturn (§12.1.7)

**ep=make_exception_ptr(e) ep** is an **exception_ptr** to exception **e**; noexcept

An **exception_ptr** can point to any exception, not just exceptions from the **exception** hierarchy. Think of **exception_ptr** as a smart pointer (like **shared_ptr**) that keeps its exception alive for as long as an **exception_ptr** points to it. That way, we can pass an **exception_pointer** to an exception out of a function that caught it and re-throw elsewhere. In particular, an **exception_ptr** can be used to implement a re-throw of an exception in a different thread from the one in which the exception was caught. This is what **promise** and **future** (§42.4) rely on. Use of **rethrow_exception()** on an **exception_ptr** (from different threads) does not introduce a data race.

The **make_exception_ptr()** could be implemented as:

```
template<typename E>
exception_ptr make_exception_ptr(E e) noexcept;
try {

throw e;
}
catch(...) {

return current_exception();
}
```

A **nested_exception** is class that stores an **exception_ptr** obtained from a call of **current_exception()**:

# nested_exception (§iso.18.8.6)

**nested_exception ne {};** Default constructor: **ne** holds an **exception_ptr** to the **current_exception()**; noexcept

**nested_exception ne {ne2};** Copy constructor: both **ne** and **ne2** hold an **exception_ptr** to the stored exception

**ne2=ne** Copy assignment: both **ne** and **ne2** hold an **exception_ptr** to the stored exception

**ne.~nested_exception()**

Destructor; virtual  
Rethrow **ne**’s stored exception;  
**terminate()** if no exception is stored in **ne**; noreturn

**ep = ne.nested_ptr()**  
**throw_with_nested(e)**  
**ep** is an **exception_ptr** pointing to **ne**’s stored exception; noexcept Throw an exception of type derived from **nested_exception** and **e**’s type; **e** must not be derived from **nested_exception**; noreturn

**rethrow_if_nested(e) dynamic_cast<const nested_exception&>(e).rethrow_nested();**  
**e**’s type must be derived from **nested_exception** The intended use of **nested_exception** is as a base class for a class used by an exception handler to pass some information about the local context of an error together with a **exception_ptr** to the exception that caused it to be called. For example:

```cpp
struct My_error : runtime_error {
  My_error(const string&);
  // ...
};
void my_code() {
  try {
    // ...
  }
  catch (...) {
    My_error err {"something went wrong in my_code()"};
    // ...
    throw_with_nested(err);
  }
}
```

Now **My_error** information is passed along (rethrown) together with a **nested_exception** holding an **exception_ptr** to the exception caught.  
Further up the call chain, we might want to look at the nested exception:

```cpp
void user()
{
  try { my_code();
  }
  catch(My_error& err) {
    // ... clear up My_error problems ...

    try { rethrow_if_nested(err); // re-throw the nested exception, if any
    }
    catch (Some_error& err2) {
```

```
// ... clear up Some_error problems ...
}
}
}
```

This assumes that we know that **some_error** might be nested with **My_error**. An exception cannot propagate out of a **noexcept** function (§13.5.1.1).

## 30.4.1.3 terminate()

In <exception>, the standard library provides facilities for dealing with unexpected exceptions:

**Section 30.4.1.3 terminate() 873**
**terminate (§iso.18.8.3, §iso.18.8.4)**
**h=get_terminate()** h is the current terminate handler; noexcept
**h2=set_terminate(h)** h becomes the current terminate handler; h2 is the previous terminate handler; noexcept **terminate()** Terminate the program; noreturn; noexcept
**uncaught_exception()** Has an exception been thrown on the current thread and not yet been caught? noexcept

Avoid using these functions, except very occasionally **set_terminate()** and **terminate()**. A call of **terminate()** terminates a program by calling a terminate handler set by a call of **set_terminate()**. The – almost always correct – default is to immediately terminate the program. For fundamental operating system reasons, it is implementation-defined whether destructors for local objects are invoked when **terminate()** is called. If **terminate()** is invoked as the result of a **noexcept** violation, the system is allowed (important) optimizations that imply that the stack may even be partially unwound (§iso.15.5.1).

It is sometimes claimed that **uncaught_exception()** can be useful for writing destructors that behave differently depending on whether a function is exited normally or by an exception. However, **uncaught_exception()** is also true during stack unwinding (§13.5.1) after the initial exception has been caught. I consider **uncaught_exception()** too subtle for practical use.

## 30.4.2 Assertions

The standard provides:
**static_assert(e,s) assert(e)**
**Assertions (§iso.7)**

Evaluate **e** at compile time; give **s** as a compiler error message if !e If the macro **NDBUG** is not defined, evaluate **e** at run time
and if !e, write a message to **cerr** and **abort()**;if **NDBUG** is defined, do nothing

For example:

```
template<typename T>
void draw_all(vector<T*>& v) {
static_assert(Is_base_of<Shape,T>(),"non-Shape type for draw_all()");
```

```
for (auto p : v) {
assert(p!=nullptr);
// ...
}
}
```

The **assert()** is a macro found in <cassert>. The error message produced by **assert()** is implementation-defined but should contain the source file name (__FILE__), and the source line number (__LINE__) containing the **assert()**.

Asserts are (as they should be) used more frequently in production code than in small illustrative textbook examples.

The name of the function (__func__) may also be included in the message. It can be a serious mistake to assume that the **assert()** is evaluated when it is not. For example, given a usual compiler setup, **assert(p!=nullptr)** will catch an error during debugging, but not in the final shipped product.

For a way to manage assertions, see §13.4.

## 30.4.3 system_error

In <system_error>, the standard library provides a framework for reporting errors from the operating system and lower-level system components. For example, we may write a function to check a file name and then open a file like this:

```
ostream& open_file(const string& path)
{
auto dn = split_into_directory_and_name(path); // split into {path,name}
error_code err {does_directory_exist(dn.first)}; // ask “the system” about the path if
(err) { // err!=0 means error
// ... see if anything can be done ...
if (cannot_handle_err)
throw system_error(err); }
// ...
return ofstream{path};
}
```

Assuming that “the system” doesn’t know about C++ exceptions, we have no choice about whether to deal with error codes or not; the only questions are “where?” and “how?” In <system_error>, the standard library provides facilities for classifying error codes, for mapping system-specific error codes into more portable ones, and for mapping error codes into exceptions:

- error_code
- error_category
- system_error error_condition
- errc
- future_errc io_errc
