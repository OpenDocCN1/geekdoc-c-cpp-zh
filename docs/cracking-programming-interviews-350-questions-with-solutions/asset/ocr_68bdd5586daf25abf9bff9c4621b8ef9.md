```
```
i : 100
i : 200
```
```

Because pseudo destructors require the syntax for explicitly calling a destructor for a nonclass type to be valid, we can write code without having to know whether or not a destructor exists for a given type.

# **Question 63** Dynamic Cast

What is *Dynamic Cast*?

# Solution of Question 63

*dynamic_cast<T>(v)* is the result of converting the expression *v* to type *T*, where *T* is

+   - a pointer or reference to complete class type, or
+   - pointer to const/volatile void.

Please note that it doesn't cast away the constness.

+   1. If T is a pointer type, then v is a prvalue of a pointer to complete class type ⇒ the result is a prvalue of type T.
+   2. If T is an lvalue reference type, then v is an lvalue of a complete class type ⇒ the result is an lvalue of the type referred to by T.
+   3. If T is an rvalue reference type, then v is an expression having a complete class type ⇒ the result is an xvalue of the type referred to by T.
+   4. If the type of v is the same as T, or it is the same as T except that the class object type in T is more cv-qualified than the class object type in v, the result is v (converted if necessary).
+   5. If the value of v is a null pointer value in the pointer case, the result is the null pointer value of type T.

# **Question 64** Dynamic Cast vs Base/Derived

How *Dynamic Cast* operates in case of Base/Derived class scenarios?

# Solution of Question 64

Let us assume that B is a base class of D.

+   - If T is a pointer type to B and v is pointer to D, then the result is a pointer to the unique subobject of the D object pointed to by v.