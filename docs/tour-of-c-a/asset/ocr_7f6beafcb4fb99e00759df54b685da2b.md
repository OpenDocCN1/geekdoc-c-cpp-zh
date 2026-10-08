```
)}
```

Given definition, the compiler will choose the move constructor to implement the transfer of the return value of the function. This means that r=x+y+z will involve no copying of Vectors.
Instead, Vectors are just moved.

As is typical, Vector's move constructor is trivial to define:

# Click here to view code image

```
Vector::Vector(Vector&& a)    "grab the elements" from a
    :elem(a.elem)
    sz(a.sz)
{
    a.elem = nullptr;      Il now has no elements
    a.sz = 0;
}
```

The && "rv reference" is a reference to which we can bind a value. The word "rvalue" is intended to complement "lvalue", which means "something that can appear on the left-hand side of an assignment" [Stroustrup,2010]. is – to a first approximation – an rvalue is a value that you cannot assign to, such as an argument returned by a function. Thus, an rvalue is a reference to something that nobody else can assign to, so we can safely "steal" its value. The res variable in operator+() for Vectors is an example.

A move constructor does not take a const argument: after, a constructor is supposed to remove the value from its argument. A move argument is defined similarly.

A move operation is applied when an rvalue reference is used as an initializer or as the right-hand of an assignment.

After a move, the moved-from object should be in a state that allows a destructor to be run. Typically, we also allow assignment to a moved-from object. The standard-library algorithms (Chapter 13) assume that. Our Vector does.

Where the programmer knows that a value will not be used again, but the compiler can't be expected to be smart enough to figure that out, the programmer can specific:

# Click here to view code image

The standard-library function move() doesn't actually move anything. Instead, it returns a reference to its argument from which we may move – an rvalue reference; it is a kind of cast ($5.2.3).

Just before we have: