```
```
bool less_than(T a, T b) {
    return a < b;
}

int main() {
    std::cout << std::boolalpha;
    std::cout << less_than(2, 3) << '\n';
    std::cout << less_than(2.2, 2.7) << '\n';
    std::cout << less_than(2.7, 2.2) << '\n';

    std::string word1 = "ABC", word2 = "XYZ";
    std::cout << less_than(word1, word2) << '\n';
    std::cout << less_than(word2, word1) << '\n';
}
```
```

The output of Listing 19.2 (templatelessthan.cpp) is

```
```
true
true
false
true
false
```
```

In the less_than function definition:

```
```
template <typename T>
bool less_than(T a, T b) {
    return a < b;
}
```
```

template and typename are reserved words, and T is a type parameter. The template keyword indicates that the function definition that follows is not a normal function definition but rather is a pattern or template from which the compiler can attempt to produce the correct function definition. A function template is also known as a generic function. The typename keyword indicates that the identifier that follows (in this case T) is a placeholder for a C++ type name. The type parameter T stands for an actual type to be determined elsewhere. T is an identifier and so can have any name legal for a variable, function, or class; some programmers prefer more descriptive names such as CompareType or TypeParam. Single capital letters such as T, S, U, and V are popular type parameter names among C++ programmers. Just as a regular parameter of a function or method represents a value, a template parameter represents a type.

You may use the reserved word class interchangeably with the keyword typename in this context:

```
```
template <class T>
bool less_than(T a, T b) {
    return a < b;
}
```
```

In Listing 19.2 (templatelessthan.cpp) the compiler generates three different less_than functions: one that accepts two integers, one that accepts two double-precision floating-point values, and one the accepts two string objects. Although the programmer cannot see them in the source code, the compiler in effect creates the following literal function definitions:

```
```
bool less_than(int a, int b) {
    return a < b;
}
```
```