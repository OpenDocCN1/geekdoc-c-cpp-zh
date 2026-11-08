
### 22.6 The Main Program

The conclusion is then formed in `main()` from Listing 22.4. You will not encounter any surprises. You need to close the anonymous namespace opened in the first listing, then `main` begins.

A comprehensive `try-catch` handles any exceptions that you might have thrown elsewhere in the program. `ex.what()` outputs an appropriate error message.

The `fName` vector stores all command-line arguments, which the `for` loop then iterates over. In it, `pack()` calls the compression function.

```cpp
// https://godbolt.org/z/5bVwX6zPdP
// } namespace
int main(int argc, const char* argv[]) {
    try {
        const std::vector<std::string> fNames {argv+1, argv+argc};
        for(auto fName : fNames) {
            std::cout << "packing " << fName << "...";
            pack(fName, fName + ".gz");
            std::cout << fName << ".gz" << "\n";
        }
    }
    catch(std::runtime_error& exc) {
        std::cerr << "Error: " << exc.what() << "\n";
    }
}
```

**Listing 22.4.** With “main” in “gzpack.cpp”, the example is complete.

### 22.7 Summary

Let’s conclude with a brief recap:

- Virtually every third-party extension consists of a library and headers.
- Include the header(s) with `#include`.
- Look at the parameters and return types of the functions and choose the appropriate C++ ones.
- Texts in `const char*` or `char*` can usually be provided using `string`.
- Large dynamic data sets with a raw pointer interact well with `vector`, `unique_ptr`, or `shared_ptr`.
- Specifically, look out for function pairs for resource management and consider managing them with a wrapper class or a custom deleter function via `shared_ptr` using C++ language features.

## Chapter 23 Templates

**Chapter Telegram**

- **Template**: A class template or function template.
- **Function template**: A template that takes a type as a template parameter to become a function.
- **Template function**: A complete function that is instantiated from a function template.
- **Class template**: Synonym for a parameterized type.
- **Template parameter**: A type that is fixed at compile time for a template; instead of a type, a template parameter can also be a constant number.
- **Parameterized type**: A class that takes another type (or a constant number) as a template parameter.
- **Instantiate template**: The moment of using a template with specific types (or constants); the compiler generates the program code at this moment.
- **Concept**: The concept language element allows templates to be constrained. This can make templates more consistent and generally leads to more understandable compiler error messages.
- **Function parameter, callback, or callback function**: A function that is passed as a parameter to a “worker function” and then called within the worker function.
- **C function pointer**: Pass a function parameter by address to a previously defined function.
- **`function<>`**: The C++ type of a function parameter.
- **Function object or functor**: A class that defines `operator()`, or an instance of it.
- **Anonymous function or lambda expression**: A locally defined function without a name.
- **Capture clause**: List of outer variables that you can access from within a lambda expression.
- **Formal data type**: The type parameter in a template declaration.
- **User-defined literal**: When you override `operator""`, you define a suffix for custom character or numeric literals.
- **Fold expression**: Within a template with a variable number of arguments, the use of an operator like `+` or `|` together with `...`, which the compiler automatically concatenates.

I won't hide it: templates are difficult. But I want to make it easy for you, because if you completely avoid templates, you will miss out on most of the good things in C++.

The good news: You don't need to fully understand templates to use them. I would even argue that there are few people who have completely understood templates. However, you can still use them without too much mental gymnastics and thus get the most benefit from them. In fact, *you have* already used templates—namely, `string`. And I very much hope that you have come to know and love `string` by now. The second faithful companion through most pages of this book, with whose help you have already used templates, is `vector`—in its `vector<int>`, `vector<double>`, or even `vector<Car>` form.

So you have already dealt with the first aspect of templates: you use them as *parameterized types*. And that's exactly what a *template* is: a class that takes another type as a parameter is a *class template*. `vector` is one of them, and so is `basic_string`. Give `basic_string` a `char` as a parameter, and you get this:

```cpp
using string = basic_string<char>;
```

Voilà! This is simplified, because `basic_string` can do a bit more. I will explain how to create templates—the class templates—once you have learned about function templates.

### 23.1 Function Templates

The second aspect of templates is function templates. Here, it is not a new class that takes a type as a parameter, but a function. You will learn this part just as quickly as using `string` and `vector`, because what you will be doing here is also not new: you are overloading functions. I will begin the explanation with this topic.

#### 23.1.1 Overloading

Strictly speaking, a function parameter consists of two parts: the *value* and its *type*. At runtime, you can call a function with different *values*: sometimes with 5, sometimes with 42, sometimes with -10. However, the *type* always remains the same.

A function where the type itself or variable is called a *function template*. Here, you must specify the type of a parameter in addition to its value when calling.

But first, let's consider a normal function like this:

```cpp
void print(int value) {
    cout << value;
}
```

You call it at runtime with the following:

```cpp
print(5);
print(42);
print(-10.25);
```

Here, the *value* of the parameter changes. Even if you pass a *double* value like in `print(-10.25)`, void `print(int)` is still called, and the parameter -10.25 is converted to an *int* value -10 for the call. So, for the last line, -10 would be output instead of -10.25.

This is not a problem for you, because you can write a function overload for the *double* type:

```cpp
void print(double value) {
    cout << value;
}
```

With this additional definition of `print(double)`, you also get the output -10.25. What do you get for the following line?

```cpp
print("Flamingo");
```

You get an error message stating that there is no suitable overload for `const char[]`. Said and done:

```cpp
void print(const char* value) {
    cout << value;
}
```

And now `print("Flamingo")` works as well. But I’m starting to notice that the function body is always the same. It always says `{ cout << value; }`. If the program gets more types that you want to output to cout with `print()`, it becomes tedious. You also get a lot of code duplication, and you should avoid that.

#### 23.1.2 A Type as Parameter

If you write it in such a way that the type is also flexible, it looks like this:

```cpp
template<typename TYPE>
void print(TYPE value) {
    cout << value;
}
```

One could say the function now has two parameters: TYPE for the type of the argument and value for its value.

When calling it specifically, you now need to specify both things. As such, you write the type argument after the function name in angle brackets:

```cpp
print<int>(5);
print<double>(-10.25);
print<const char*>("Flamingo");
```

But the compiler already knows that 5 is an int, -10.25 is a double, and "Flamingo" is a const char*. And when the compiler can make the choice for you, you can also omit the angle brackets and the explicit type when calling this function:

```cpp
print(5);
print(-10.25);
print("Flamingo");
```

These lines are equivalent to the previous example. However, it is important to note that you now actually have three functions: one for int as a parameter, one for double, and one for const char*.

Note that whether you write `template<typename TYPE>` or `template<class TYPE>` is irrelevant. Both notations are equivalent, and it is a matter of taste or agreement to use one or the other. The standard library prefers class here, while I personally prefer typename.

#### 23.1.3 Function Body of a Function Template

The function body of print takes advantage of the fact that the output operator operator<< is defined for int, double, and const char*. This is, of course, not true for all types.

```cpp
// https://godbolt.org/z/aMP3jK7EE
#include <iostream>
struct Number {
    int value;
};
template<typename TYPE>
void print(TYPE value) {
    std::cout << value << "\n";
}
```
