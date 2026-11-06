The next step is to implement the corresponding overloaded binary assignment operator, having the form @=, with @ being a binary operator. As this operator always has a left-hand operand which is an object of its own class, it is implemented as a true member function. Furthermore, the binary assignment operator should return a reference to the object to which the binary operation applies, as the object might be modified in the same statement. E.g., (s2 += s3) + " postfix". Here is our second revision of the class Binary, showing both the declaration of the plain binary operator and the corresponding binary assignment operator:

```
```cpp
class Binary
{
    public:
        Binary();
        Binary(int value);

        Binary &operator+=(Binary const &rhs);
};

Binary operator+(Binary const &lhs, Binary const &rhs);
```
```

How should the binary assignment operator be implemented? When implementing the binary assignment operator the strong guarantee should again be kept in mind. Use a temporary object and swap if the binary operation might throw. Example:

```
```cpp
Binary &operator+=(Binary const &other)
{
    Binary tmp(*this);
    tmp.add(other);     // this may throw
    swap(tmp);
    return *this;
}
```
```

It's easy to implement the plain binary operator for classes offering the matching binary assignment operator: the lhs argument is copied into a Binary tmp to which the rhs operand is added. Then tmp is returned. The copy construction and two statements could be contracted into one single return statement, but then compilers usually aren't able to apply copy elision in this case. But copy elision is usually used when the steps are taken separately:

```
```cpp
class Binary
{
    public:
        Binary();
        Binary(int value);

        Binary &operator+=(Binary const &other);
};

Binary operator+(Binary const &lhs, Binary const &rhs)
{
    Binary tmp(lhs);
    tmp += rhs;
    return tmp;
}
```
```

But wait! Remember the design principle for move-aware classes that was given in section 9.7.8? When implementing binary operators we're doing exactly that what was mentioned in that design principle. A temporary object is constructed and the binary assignment operation is applied to the temporary object.

If the class Binary is a move-aware class then we can add a move-aware binary operator to our class