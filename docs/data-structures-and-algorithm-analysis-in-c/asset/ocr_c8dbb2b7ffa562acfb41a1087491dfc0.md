# # Address-of Operator (&)

One important operator is the **address-of operator** &. This operator returns the memory location where an object resides and is useful for implementing an alias test that is discussed in Section 1.5.6.

# ## 1.5.2 Lvalues, Rvalues, and References

In addition to pointer types, C++ defines reference types. One of the major changes in C++11 is the creation of a new reference type, known as an rvalue reference. In order to discuss rvalue references, and the more standard value reference, we need to discuss the concept of lvalues and rvalues. Note that the precise rules are complex, and we provide a general description rather than focusing on the corner cases that are important in a language specification and for compiler writers.

An **lvalue** is an expression that identifies a non-temporary object. An **rvalue** is an expression that identifies a temporary object or is a value (such as a literal constant) not associated with any object.
As examples, consider the following:

```
vector<string> arr( 3 );
const int x = 2;
int y;
...
int z = x + y;
string str = "foo";
vector<string> *ptr = &arr;
```

With these declarations, arr, str, arr[x], &x, y, z, ptr, *ptr, (*ptr)[x] are all lvalues. Additionally, x is also an lvalue, although it is not a modifiable lvalue. As a general rule, if you have a name for a variable, it is an lvalue, regardless of whether it is modifiable.

For the above declarations 2, "foo", x*y, str.substr(0,1) are all rvalues. 2 and "foo" are rvalues because they are literals. Intuitively, x*y is an rvalue because its value is temporary; it is certainly not x or y, but it is stored somewhere prior to being assigned to z. Similar logic applies for str.substr(0,1).

Notice the consequence that there are some cases in which the result of a function call or operator call can be an lvalue (since *ptr and arr[x] generate lvalues) as does cin>>x>>y and others where it can be an rvalue, hence, the language syntax allows a function call or operator overload to specify this in the return type, and this aspect is discussed in Section 1.5.4. Intuitively, if the function call computes an expression whose value does not exist prior to the call and does not exist once the call is finished unless it is copied somewhere, it is likely to be an rvalue.

A reference type allows us to define a new name for an existing value. In classic C++, a reference can generally only be a name for an lvalue, since having a reference to a temporary would lead to the ability to access an object that has theoretically been declared as no longer needed, and thus may have had its resources reclaimed for another object. However, in C++11, we can have two types of references: lvalue references and rvalue references.