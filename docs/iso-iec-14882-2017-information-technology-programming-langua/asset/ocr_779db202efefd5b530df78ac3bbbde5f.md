# ISO/IEC 14882:2017(E)

the rules in 16.3.1.2 determine which, if, interpretation is used.

# 16.5.3 Assignment

An assignment operator shall be implemented by a non-static member function with exactly one parameter. Because a copy assignment operator `operator=` is implicitly declared for a class if not declared by the user (15.8), a base class assignment operator is always hidden by the copy assignment operator of the derived class.

Any assignment operator, even the copy and move assignment operators, can be virtual. [Note: For a derived class D with a base class B for which a virtual copy/move assignment has been declared, the copy/move assignment operator in D does not override B's virtual copy/move assignment operator. [Example:

```
struct B {
    virtual int operator=(int);
    virtual B operator=(const B&);
};
struct D : B {
    virtual int operator=(int);
    virtual D operator=(const B&);
};

Dobjj1;
Dobjj2;
B* ptr = &dobj1;
void f() {
    ptr->operator=(99); // calls D::operator=(int)
    *ptr = 99;
    ptr->operator=(dobj2); // calls D::operator=(const B&)
    *ptr = dobj2;
    dobj1 = *ptr;
};
```

-- end example --

# 16.5.4 Function call

operator() shall be a non-static member function with an arbitrary number of parameters. It can have default arguments.

```
postfix-expression <expression-list_opt>
```

where the `postfix-expression` evaluates to a class object and the possibly empty `expression-list` matches the parameter list of `operator()` member function. Thus, a `x(arg1, ...)` is interpreted as `x.operator(arg1, ...)` for a class x of type T if `operator()(T1, T2, T3)` exists and if the operator is selected as the best match by the overload resolution mechanism (16.3.3).

# 16.5.5 Subscribing

operator() shall be a non-static member function with exactly one parameter. Its syntax

```
postfix-expression <expression-braced-init-list>
```

Thus, a subscribing expression `x{y}` is interpreted as `x.operator()(y)` for a class x of type T if `operator()(T1)` exists and if the operator is selected as the best match by the overload resolution mechanism (16.3.3). [Example:

```
struct X {
    X operator()(std::initializer_list<int>);
```