
vector. However, the vector must have enough space allocated beforehand; that's why you create it with the length constructor argument in the appropriate size.

Besides vector, only array has such a data() method. No other standard container guarantees that its data is contiguous, allowing it to be read in one go with read() and similar functions.

A word about return data, where the return type is vector<char>—a value, not a reference or pointer. Potentially, returning such a value type could require a large copy operation. However, the compiler and the standard mandated library work together here to “avoid the copy” (copy elision). This is guaranteed in this case because all return statements within the function return the same local variable; here it's trivial because there's only a single return. In this case, the compiler never needs to create a copy for the return, even if it is returned by value. Before the standard copy elision in this situation, this scenario was commonly referred to as return value optimization (RVO).

The pack() function starts with two trivial lines. The first line, readFile(), reads the input, and the second line, GzWriteStream gz, prepares the output. This is done using the overloaded operator<<. For simplicity, I implemented it as a method. A free friend function would have been possible as well, but it is not necessarily needed here as the stream class is under—unlike ostream, where you can only work with a free function overload of operator<<.

## 22.6 The Main Program

The conclusion is then formed by main() from Listing 22.4. You will not encounter any surprises. You need to close the anonymous namespace opened in the first listing, then main begins.

A comprehensive try-catch handles any exceptions that you might have thrown elsewhere in the program. exc.what() outputs an appropriate error message.

The fName vector stores all command-line arguments, which the for loop then iterates over. In it, pack() calls the compression function.

```cpp
// https://godbolt.org/zSb x6PzdP
// namespace
int main(int argc, const char* argv[]) {
    try {
        const std::vector<std::string> fName{argv+1, argv+argc};
        for(auto fName : fName) {
            std::cout << "packing " << fName << " ...";
            pack(fName, fName+".gz");
            std::cout << fName << ".gz" << "\n";
        }
    } catch (std::runtime_error &exc) {
        std::cerr << "Error: " << exc.what() << "\n";
    }
}
```

**Listing 22.4** With "main" in "gzippack.cpp", the example is complete.

## 22.7 Summary

Let’s conclude with a brief recap:

- Virtually every third-party extension consists of a library and headers.
- Include the header(s) with #include.
- Look at the parameters and return types of the functions and choose the appropriate C++ ones.
- Texts in const char* or char* can usually be provided using string.
- Large dynamic data sets with a raw pointer interact well with vector, unique_ptr, Or shared_ptr.
- Specifically, look out for function pairs for resource management and consider managing them with a wrapper class or a custom deleter function via shared_ptr using C++ language features.

## 23 TEMPLATES

## Chapter Telegram

- **Template**: A class template or function template.
- **Function template**: A template that takes a type as a template parameter to become a function.
- **Template function**: A complete function that is instantiated from a function template.
- **Class template**: Synonym for a parameterized type.
- **Template parameter**: A type that is fixed at compile time for a template; instead of a type, a template parameter can also be a constant number.
- **Parameterized type**: A class that takes another type (or a constant number) as a template parameter.
- **Instantiate template**: The moment of using a template with specific types (or constants); the compiler generates the program code at this moment.
- **Concept**: The concept language element allows templates to be constrained. This can make templates more consistent and generally leads to more understandable compiler error messages.
- **Function parameter, callback, or callback function**: A function that is passed as a parameter to a "worker function" and then called within the worker function.
- **C function pointer**: Pass a function parameter by address to a previously defined function.
- **function<>**: The C++ type of a function parameter.
- **Function object or functor**: A class that defines operator(), or an instance of it.
- **Anonymous function or lambda expression**: A locally defined function without a name.
- **Capture clause**: List of outer variables that you can access from within a lambda expression.
- **Formal data type**: The type parameter in a template declaration.
- **User-defined literal**: When you override operator"", you define a suffix for custom character or numeric literals.
- **Fold expression**: Within a template with a variable number of arguments, the use of an operator like + or | together with ..., which the compiler automatically concatenates.

## 23.1 Function Templates

The second aspect of templates is function templates. Strictly speaking, a function parameter consists of two parts: the value and its type. At runtime, you can call a function with different values: sometimes with 5, sometimes with 42, sometimes with -10. However, the type always remains the same. A function where the type itself is variable is called a function template: Here, you must specify the type in addition to its value.

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

Here, the value of the parameter changes. Even if you pass a double value like in print(-10.25), void print(int) is still called, and the parameter -10.25 is converted to an int value -10. So, for the last line, -10 would be output instead of -10.25.

This is not a problem for you, because you can write a function overload for the double type:

```cpp
void print(double value) {
  cout << value;
}
```

With this additional definition of print(double), you also get the output -10.25. What do you get for the following line?

```cpp
print("Flamingo");
```

You get an error message stating that there is no suitable overload for const char[]. Said and done:

```cpp
void print(const char* value) {
  cout << value;
}
```

And now print("Flamingo"); works as well. But I'm starting to notice that the function body is always the same. It always says { cout << value; }. If the program gets more types that you want to output to cout with print(), it becomes tedious. You also get a lot of code duplication, and you should avoid that.

## 23.1.2 A Type as Parameter

If you write it in such a way that the type is
