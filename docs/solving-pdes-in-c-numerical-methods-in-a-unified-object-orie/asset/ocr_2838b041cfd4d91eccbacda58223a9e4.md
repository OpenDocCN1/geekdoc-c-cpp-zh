```
int main() {
	point P;
	printf("P.x=%f\n", P.zero()->X());
	return 0;
} // print P.x after P has been set to zero
```

Here, the function "printf" prints the 'x'-field of the "point" object 'P' whose address is returned by the "zero()" function.

Later on, we'll show how the "zero" function can also be rewritten as a "friend" function. The reserved word "friend" should then precede the function name in the declaration in the class block. No current object or "this" pointer is available; objects must be passed explicitly as arguments, as in ordinary functions. Next, we'll see that arguments should be passed not by name (or value) but rather by reference.

# 2.9 References

In C++, one can define a reference to a variable. A reference is actually another name for the same variable. For example,

```
point p;
point& q = p;
```

defines a variable 'q' of type reference-to-point, initialized to refer to the "point" object 'p'. (Because 'q' is a reference, it must be initialized.) Every change to 'q' affects 'p' as well, and vice versa.

In the previous chapter, we saw that if a function is supposed to change a variable, then this variable must be passed to it by address, that is, by passing a pointer argument that points to it. A more transparent method is to pass a reference to this variable, which allows the function to refer to it and change it. For example, the above "zero" function can also be implemented as a friend function, which sets its argument to zero. This is done as follows.

```
friend const point* zero(point&);
```

The actual definition can be made outside the block of the "point" class:

```
const point* zero(point&p){
	p.x=p.y=0.;
	return &p;
} // set "point" argument to zero
```

With this implementation, the function "zero" can be declared as a friend of other classes as well, so it can also use their private fields, if necessary. In the present example, this is not needed, so one can actually declare and define the function at the same time inside the block of the "point" class as follows:

```
friend const point* zero(point&p){
	p.x=p.y=0.;
	return &p;
} // declare as friend and define
```