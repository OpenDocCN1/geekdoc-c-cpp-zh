
### Abbreviated Function Templates

The syntax to introduce a template is quite verbose. Just take a look at the following straightforward template for functions that square their input:

```cpp
template <typename T>    // ?? Do we really need this?
auto sqr(T x) { return x * x; }
```

It takes two eight-letter keywords, template and typename, to declare a single template type parameter T. C++20 allows us to write such templates much more compactly, as follows:

```cpp
auto sqr(auto x) { return x * x; }
```

This syntax is a natural extension of the syntax you use to request function return type deduction. Before, you could only use the auto keyword as a placeholder for a function’s return type, but now you can use it as a placeholder for function parameter types as well. Of course, other placeholder types such as auto*, auto&, and const auto& are allowed as well. For instance:

```cpp
auto cube(const auto& x) { return x * x * x; }
```

Even though the sqr() and cube() definitions now no longer use the template keyword, they both remain function templates. In fact, semantically, our second definition of sqr() is, in every single way, completely equivalent to our original definition. The only difference is that the new syntax is shorter. Hence the name: abbreviated function template. The fact that sqr(), for instance, is a function template implies that the compiler always needs access to its definition in every compilation unit where you invoke it (we discuss this further in the next chapter). It also implies that you can explicitly instantiate it (sqr<int>(...)), specialize it (template <> auto sqr(int x)), and so on, should you ever need to.

Every occurrence of auto in the function parameter list of an abbreviated function template effectively introduces an implicit, unnamed template type parameter. The following two prototypes are therefore completely equivalent (notice how the auto in the function return type does not give rise to an additional template parameter):

```cpp
const auto& larger(const auto& a, const auto& b);
```

```cpp
template <typename T1, typename T2>
const auto& larger(const T1& a, const T2& b);
```

You are even allowed to mix both notations, as shown in this artificial example:

```cpp
// A function template with two template type parameters: one explicit and one implicit
template <typename T>
const T& mixAndMatch(auto* mix, const T& match1, const T& match2);
```

### Limitations to Abbreviated Function Templates

If you want your template to instantiate functions where multiple parameters have the same type or related types, you still have to use the old syntax.

```cpp
template <typename T>
const T& larger(const T& a, const T& b);
```

Similarly, if you need to refer to one of the parameter type names elsewhere—for instance in the function body—it often remains easier to stick with the old syntax.

```cpp
// Create a vector containing consecutive values in the range [from, to)
template <typename T>
auto createConsecutiveVector(const T& from, const T& to)
{
    std::vector<T> result;
    for (T t = from; t < to; ++t)
        result.push_back(t);
    return result;
}
```

### Summary

In this chapter, you learned how to define your own parameterized templates for functions and how to instantiate them to create functions. This allows you to create functions that work correctly and efficiently for any number of related types. The important bits that you should take away from this chapter are as follows:

- A function template is a parameterized recipe used by the compiler to generate overloaded functions.
- The parameters in a function template can be type parameters or non-type parameters. The compiler creates an instance of a function template for each function call that corresponds to a unique set of template parameter arguments.
- A function template can be overloaded with other functions or function templates.
- Placeholder types such as `auto`, `const auto&`, and `auto*` can not only be used to enable return type deduction for a function—which can be particularly useful in function templates, as it happens—but when used as the type of a function parameter, they also introduce so-called abbreviated function templates.

### EXERCISES

These exercises enable you to try some of what you've learned in this chapter. If you get stuck, look back over the chapter for help. If you're still stuck, you can download the solutions from the Apress website (www.apress.com/source-code), but that really should be a last resort.

- **Exercise 10-1.** In C++17, the Standard Library `<algorithm>` module gained the handy `std::clamp()` function template. The expression `clamp(a,b,c)` is used to clamp the value `a` to a given closed interval `[b,c]`. That is, if `a` is less than `b`, the result of the expression will be `b`; and if `a` is greater than `c`, the result will be `c`; otherwise `a` lies within the interval `[b,c]` and `clamp()` simply returns `a`. Write your own `my_clamp()` function template and try it with a little test program.
- **Exercise 10-2.** After the last lines of `Ex10_01`'s `main()` function as follows:

```cpp
const auto a_string = "A", z_string = "Z";
std::cout << "larger of " << a_string << " and " << z_string
          << " is " << larger(a_string, z_string) << std::endl;
```

If you now run the program, you may very well get the following output (if not, try rearranging the order in which a_string and z_string are declared):

```
Larger of 1.5 and 2.5 is 2.5
Larger of 3.5 and 4.5 is 4.5
Larger of 17011983 and 10 is 17011983
Larger of A and Z is A
```

What's that? "A" is larger than "Z"? Can you explain what went wrong? Can you fix it?

Hint. To compare two character arrays, you could perhaps first convert them to another string representation.

- **Exercise 10-3.** Write a function template called plus() that takes two arguments of potentially different types and returns a value equal to the sum of both arguments. Next, make sure that plus() can be used as well to add the values pointed to by two given pointers.

Extra: Can you now make it so that you can also concatenate two string literals using plus()?
Warning: This may not be as easy as you think!

- **Exercise 10-4.** Write your own version of the std::size() family of functions called my_size() that work not only for fixed-size arrays but also for std::vector<> and std::array<> objects. You are not allowed to use the sizeof() operator.
- **Exercise 10-5.** Can you think of a way to verify that the compiler generates only one instance of a function template for any given argument type? Do so for the larger() function in Ex10_01.cpp.
- **Exercise 10-6.** In Chapter 8, you studied a quicksort algorithm that worked for pointers-to-strings. Generalize the implementation of Ex8_18.cpp so that it works for vectors of any type (any type for which the < operator exists, that is). Write a main() function that uses this to sort some vectors with different element types and outputs both the unsorted and sorted element lists. Naturally, you should do this by also creating a function template that streams vectors with arbitrary element types to std::cout.

## CHAPTER 11

## Modules and Namespaces

While cramming all your code into a single source file is always possible (even for huge programs), a larger code base is far easier to manage if you organize related source code (functions, constants, types, and so on) into logical, composable units, each in their own files. Not least because you and others can then construct different applications out of these same building blocks. As of C++20, the composition unit of choice is a *module*.

The more your code base grows and/or the more third-party libraries you rely on, the more likely it becomes to have two functions, two global variables, two types, and so on, with the same name. Perhaps two independent subsystems inadvertently define their own `log()` or `validate()` functions, for instance, or their own ErrorCode enumeration types. Because real-life code bases easily span millions of lines of code, with each subsystem mostly developed by semi-autonomous teams, it is virtually impossible to avoid *name clashes* or *name collisions* without some agreed upon hierarchical naming scheme. In C++, the recommended approach is that different subsystems declare their names in disjoint *namespaces*.

In this chapter, you’ll learn about:

- How to build composable units of code in the form of modules
- How to export entities from a module so that they can be used in any source file that imports that module
- How to split larger modules into smaller, more manageable units
- The difference between module partitions and submodules
- More about using namespaces and how to define and manage your own
- The relation between modules and namespaces
- How to split a component’s interface from its implementation at the level of both modules and namespaces

### Modules

At the lowest level of granularity, any C++ program is pieced together from elementary, reusable entities such as functions, types, and variables.

And for really small programs—such as the ones you wrote so far—that may be all you need within your own code.

But as your code base starts growing, you’ll soon notice that you also need some other mechanism to further organize your code at a higher level of granularity. You’ll want to group related functionality together, so that you and everyone else knows where to look for it. You’ll want to decompose your program into larger, discrete subcomponents, where each component solves one specific piece of the puzzle.

Internally, these subcomponents can then use whatever combination
