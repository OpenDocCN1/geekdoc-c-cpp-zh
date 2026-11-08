```
int calculate(int a, int b, std::function<int(int,int)> binop) {
    return binop(a,b);
}
int plus(int a, int b) { return a+b; }
int times(int a, int b) { return a*b; }
int main() {
    std::cout << calculate(3, 4, plus) << "\n";  // Output: 7
    std::cout << calculate(3, 4, times) << "\n";  // Output: 12
}
```

**Listing 23.13** Use the name of a suitable function as a function parameter.

That's all. The plus and times functions, instances of type `function<int(int, int)>`, are passed to the function calculate() as parameters.

It is important that the signatures of the functions match. For example, you cannot use the negate function. The compiler complains with an error:

```
int negate(int a) { return -a; }
// ...
std::cout << calculate(3, 4, negate) << "\n"; // ⚡ wrong signature
```

# 23.3.2  C Function Pointer

In this section, I will tell you a bit about the history of C++. If your head is already spinning, you can skip it on the first read.

With my compiler, the error message is as follows:

```
could not convert 'negate' from 'int(*)(int)' to
    'std::function<int(int,int)>'
```

So negate does not appear as std::function<int(int)> but as int (*)(int). This is the actual type of a function when you pass it as a parameter. The std::function<int(int)> construct is just a C++ utility. The int (*)(int) notation comes from C times and is called a function pointer or pointer. The compiler implicitly converts a C-type function int (*)(int) to the corresponding C++-type std::function<int(int)>. Because the C notation looks very strange (at least subjectively to my eyes), I prefer the C++ notation wherever possible.

To be able to read what the compiler tells you, we need to decrypt the C type. The entire type of the function is int (*)(int):

+   - The (*) in the middle means that it is some kind of function pointer.
+   - int at the beginning is the return type of the function signature.
+   - (int) in parentheses describes the parameter types of the function signature.