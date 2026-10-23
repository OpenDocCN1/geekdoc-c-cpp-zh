# 2.10. Copy Constructor

Here, the reference to `P` returned by `P.zero()` serves as the current object in a further call to the `X()` function.

Passing arguments by reference is not only convenient but also efficient. Indeed, when the argument is passed by reference rather than by value, the need to invoke the copy constructor to construct a local copy is avoided. For example, if the "negative" function in Section 2.6 had been rewritten as

```
const point negative(const point& p){
    return point(-p.X(),-p.Y());
}   //  passing argument by reference
```

then no local "point" object would be constructed, only a local reference to the concrete argument. Creating this reference requires only copying the address of the concrete argument rather than copying the entire concrete argument physically. The total number of constructions in the call to the "negative" function would then decrease from three to two.

The "negative" function still requires two calls to constructors of "point" objects: one to construct the local negative and the other to return a copy of it. This number cannot be reduced further. Look what happens if one attempts to avoid the second construction by writing

```
const point& negative(const point& p){
    return point(-p.X(),-p.Y());
}   //  wrong!!! returns reference to nothing
```

This version returns by reference rather than by value. (Indeed, the type of function is "const point&" rather than "const point".) It returns a reference to the local variable that contains the negative of the "point" argument. However, the negative of the "point" argument is a temporary local variable, which no longer exists at the end of the function, so it actually returns a reference to nothing. One should therefore drop this version and stick to the previous one.

# 2.10  Copy Constructor

As mentioned in Section 2.6, it is good practice to define an explicit copy constructor. For example, a suitable copy constructor can be written in the block of the "point" class as follows:

```
point(const point& p):x(p.x),y(p.y){
}   //  copy constructor
```

Here, the copied "point" object is passed to the constructor by reference, and its fields are used to initialize the corresponding fields in the constructed "point" object.

Actually, it is not necessary to write this constructor, because the default copy constructor available in the C++ compiler does exactly the same thing. Still, it is good practice to write your own copy constructor, because in many cases the default one does the wrong thing, as we'll see below.

The above copy constructor is invoked whenever the compiler encounters an explicit copying such as