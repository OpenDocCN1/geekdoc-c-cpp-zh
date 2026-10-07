62

# A SKETCH OF C++

other objects using w. The first object x is a pointer to data type X we create using
this pointer for w. The second object y is a reference variable for X objects that is
initialized with a reference to*this, or equivalently, a reference to w. The final object z is
of type X but is created by dereferencing this pointer for w. The addresses are printed
out for all four objects, x, y and z are each used to change the value of their K data
produces the output

```
w address = 0xbfffa24
w.K = 1
x value = 0xbfffa24
w.K = 2
y address = 0xbfffa24
w.K = 3
z address = 0xbfffa20
w.K = 3
```

As expected, x and y serve as aliases for w. This is not true for z which lies in a different
memory location and exists independently of w. Augmenting its value for K does not
afect the value of w.K. What has happened in the creation of z is that the use of the =
operator has caused the creation of a new X object. This new object is created under the
def behavior of element-by-element copying. Specifically, a new memory location is set
aside for z and then the value of K for the object *w.getThis() is copied
in this location.

+   Note that this is a const pointer in the Section of 3.5 as illustrated in Listing 3.3.
It cannot be reassigned to another object.

# 3.8.3 const correctness

We briefly discussed the C++ keyword const in Section 3.5. The use of this modifier
imposes an additional level of type checking that finishes compile-time protection against
inadvertent changes being made to objects in one's code. The code correctness means
t const has been used anywhere where it is appropriate. It is a practice to examine
not only in terms of error protection but also by the way it forces a programmer to examine
code when the use of const is indicated. In general, using const appropriately
in no loss in functionality while providing safeguards and clarity. Our discussion of
t const keyword in this section will focus on four cases where it will arise in later sections
and chapters: const pointers, const references, const class members and const member
functions.

Due to efficiency of passing pointers or addresses over (copies of) objects, the use
situations. However, the use of addresses and pointers as function arguments carries with
it the danger that the function may alter the object being pointed to in cases when this
is not desirable. To avoid such events, a const designation can be applied for a pointer or
nference. Syntax of the form

```
const dataType& p = &;
```

creates a pointer p to a variable x where the value of x cannot be changed. Similarly,

```
const dataType& y = x;
```

accomplishes the same with a reference; that is, y is just an alias for x except that
the value that y refers to memory cannot be changed and, hence, cannot be used to
change the value of x.