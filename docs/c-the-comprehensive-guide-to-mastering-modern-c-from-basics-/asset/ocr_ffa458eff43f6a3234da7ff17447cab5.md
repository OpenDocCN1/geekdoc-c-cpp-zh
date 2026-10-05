```
john.print(); // calling the method for a variable of the
type
}
```

# Listing 12.5 Methods bundle data and behavior together.

Now print is part of the Person type and thus has become a method.

When one speaks of a method, they mean a function within a type. To be distinguished from this are functions outside of classes, which you have learned about so far.

Sometimes functions are also called free functions to distinguish them from methods. The term global functions is also sometimes used, but it is not entirely correct; a function can also be within a namespace and is still free, but not global. Conversely, the term member function is used for method.

Technically speaking, methods are also just functions. One of the differences is that the full identifier of a method includes the class name. If you define the method outside the type, then you call it—for example, Person::print. Within the method, you can then access all data fields and methods of the class without further qualification: where before you wrote p.name_, now name_ is sufficient.

Strictly speaking, the compiler internally translates to this->name—and here I come to the second important difference from functions: a method from Type always has an implicit Type* this parameter,[ 17] without it appearing in the method's parameter list. This parameter represents the memory address of the