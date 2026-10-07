Instead of your having to write many similar max () functions, wouldn't it be nice to just write one max () function that returns the greater of its two arguments and can accommodate almost any type of argument?

# Why Not Use A Macro

You can write a macro to solve this problem but you lose the ability to ensure that you are not comparing arguments of different types. For example, if your intent is to guarantee that both arguments are the same type, then a macro does not work:

```
#define max(x, y) ((x) > (y)) ? (x) : (y)
int main() {
    cout << max(1, 2.98) << endl;
    cout << max('A', 32) << endl;
    cout << max(++a, b++) << endl;
    return 0;
}
```

There is no type checking here and the arguments could be evaluated twice when using prefix or postfix notation.

# Template Functions

Template functions provide a mechanism by which the programmer can take advantage of the compactness of the macro solution without forfeiting any of the benefits of a strongly-typed language.

A function template solves the problem by allowing you to write just one function as a skeleton, or template, for a family of functions whose tasks are all similar. At the same time, full type checking is carried out.

You should consider using a function template when you find yourself writing a sequence of identical, overloaded functions. By using templates, you can define a pattern for a family of related overloaded functions by letting the data type itself be a parameter!