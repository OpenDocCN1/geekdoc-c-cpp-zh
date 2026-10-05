# 822 Introduction to C++

Note if we make the show() non-virtual in classes A and B, the C class is no longer polymorphic, and the typeof returns the static type (known at compile time) of the expression. Therefore, the if condition are false and the program displays nothing. In particular, the typeof(*p) returns the type of the B class, similarly the typeof(r) returns the type of the A class, this is the static type of *r. If p is a null pointer, the operator does not create the bad_type exception, it does not need to be a valid pointer to evaluate the type of *p.

Type identification should only be used when necessary. For example, suppose we have a hierarchy of A, B, and C classes and we want to perform some operations depending on the type of the object to which we reference:

```
void f(A& a)
{
    if (typeof(a) == typeof(A))
    {
    }
    else if (typeof(a) == typeof(B))
    {
    }
    ...
    else if (typeof(a) == typeof(C))
    {
    }
}
```

Because type identification may involve runtime overhead, this code is not so efficient. Besides that, it is not flexible since every time the class hierarchy changes (e.g., with the addition of a new class) we have to change the if clauses. Or of course, we already know it. When our code depends on the type of the object pointer to or a reference refers to, the most flexible and efficient approach is to use virtual functions.

As an example of type identification might be useful consider a class hierarchy where to overload the == operator to compare objects. Two objects are the same type and the same values in their members. It makes sense for the overload function to take as parameters two references to the base class, so derived objects can be passed safely. For example:

```
bool operator==(const Base& a, const Base& b)
{
    if (typeof(a) == typeof(b)) // First, compare the types.
    {
        // Then, compare the values of their members.
    }
}
```

# TYPE CAST OPERATORS

C++ provides operators that we can use to make type casts with more safety. For example, we saw the dynamic_cast operator. The other operators are the const_cast, static_cast, and reinterpret_cast. All of them are processed at compile time. Besides more safety, a second reason for using them is