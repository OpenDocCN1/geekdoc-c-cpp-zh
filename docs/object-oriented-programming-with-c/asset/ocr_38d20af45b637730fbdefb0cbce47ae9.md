```
constructor (arglist) : intialization-section
{ assignment-section
}
```

The _assignment-section_ is nothing but the body of the constructor function and is used to assign initial values to its data members. The part immediately following the colon is known as the _initialization section_. We can use this section to provide initial values to the base constructors and also to initialize its own class members. This means that we can use either of the sections to initialize the data members of the constructors class. The initialization section basically contains a list of initializations separated by commas. This list is known as _initialization list_. Consider a simple example:

```
class XYZ
{
int a;
int b;
public:
XYZ(int i, int j) : a(i), b(2 * j) { }
};
main()
{
XYZ x(2, 3);
}
```

This program will initialize **a** to 2 and **b** to 6. Note how the data members are initialized, just by using the variable name followed by the initialization value enclosed in the parenthesis (like a function call). Any of the parameters of the argument list may be used as the initialization value and the items in the list may be in any order. For example, the constructor **XYZ** may also be written as:

```
XYZ(int i, int j) : b(i), a(i + j) { }
```

In this case, **a** will be initialized to 5 and **b** to 2. Remember, the data members are initialized in the order of declaration, independent