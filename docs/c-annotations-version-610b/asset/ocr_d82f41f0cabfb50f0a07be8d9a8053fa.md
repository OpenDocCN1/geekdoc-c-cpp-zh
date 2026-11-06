```
```cpp
{
    cout << "Move constructor\\n";
}
Class &operator+=(Class const &rhs)
{
    cout << "operator+=\\n";
}
};

Class factory()
{
    return Class();
}

int main()
{
    Class lhs;
    Class rhs;
    Class result;

    result = lhs + rhs;
    result = factory() + rhs;

//    result = lhs - rhs;   // this won’t compile as operator-= hasn’t been
                           // defined
}
```
```

# 23.5.1  Binary operators allowing promotions

The function templates introduced in the previous section do not support promotions. E.g., a statement like

```
```cpp
result = rhs + 2;
```
```

generates a compilation error as promotions are not recognized by the template argument deduction algorithm. Currently, the above statement needs to be rewritten to have it accepted by the compiler:

```
```cpp
result = rhs + Class(2);
```
```

If promotions are welcome, how can we change the arithmetic operator function templates so that promotions are performed? With promotions the arguments of the operator functions may be of any type, at least one of them must be of the class type offering the matching arithmetic assignment operator. But when designing the function template we can’t say which of the two operands has that class type. So we have to specify two template types parameters for the two parameters of the operator functions. The function template must therefore start with something like this:

```
```cpp
template <typename LHS, typename RHS>
ReturnType operator+(LHS const &lhs, RHS const &rhs)
```
```

At this point we can’t yet specify ReturnType. It is LHS if RHS can be promoted to or is equal to LHS, it is be RHS if LHS is promoted to RHS.

To determine whether RHS can be promoted to LHS we now design a simple template meta programming class LpromotesR using two template parameters, defining the value true (1) if the second (right hand) type can be promoted to the first (left-hand) type, and defining the value false (0) if not. Here we use the same principle seen before in section 22.7.3, type convertibility: