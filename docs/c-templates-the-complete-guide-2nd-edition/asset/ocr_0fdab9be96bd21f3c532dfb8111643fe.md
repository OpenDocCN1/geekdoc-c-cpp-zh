```
stringStack.pop();
}
```

By declaring type Stack<int>, int is used as type T inside the class template. Thus, intStack is created as an object that uses a vector of ints as elements and, for all member functions that are called, code for this type is instantiated. Similarly, by declaring and using Stack<std::string>, an object that uses a vector of strings as elements is created, and for all member functions that are called, code for this type is instantiated.

Note that code is instantiated only for template (member) functions that are called. For class templates, member functions are instantiated only if they are used. This, of course, saves time and space and allows use of class templates only partially, which we will discuss in Section 2.3 on page 29.

In this example, the default constructor, push(), and top() are instantiated for both int and strings. However, pop() is instantiated only for strings. If a class template has static members, these are also instantiated once for each type for which the class template is used.

An instantiated class template’s type can be used just like any other type. You can qualify it with const or volatile or derive array and reference types from it. You can also use it as part of a type definition with typedef or using (see Section 2.8 on page 38 for details about type definitions) or use it as a type parameter when building another template type. For example: Click here to view code image

```
void foo(Stack <int> const& s) // parameter s is int stack
{
using IntStack = Stack <int>; // IntStack is another name for Stack<int>
Stack< int> istack[10]; // istack is array of 10 int stacks
IntStack istack2[10]; // istack2 is also an array of 10 int stacks (same type)
...
}
```

Template arguments may be any type, such as pointers to floats or even stacks of ints: Click here to view code image

```
Stack< float*> floatPtrStack; // stack of float pointers
Stack<Stack< int>> intStackStack; // stack of stack of ints
```

The only requirement is that any operation that is called is possible according to this type.

Note that before C++11 you had to put whitespace between the two closing template brackets: Click here to view code image