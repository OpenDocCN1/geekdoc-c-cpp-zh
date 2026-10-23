converted implicitly to a "point" object, which is then used as a concrete argument in the "negative" function.

# 2.7 Destructor

At the end of the block of a function, the local variables are destroyed, and the memory allocated for them is freed for future use. This is done by the destructor invoked implicitly by the computer. If no destructor is defined explicitly in the class block, then the default destructor available in the C++ compiler is used. This destructor goes over the data fields in the object and destroys them one by one. This is done in reverse order: "point" objects, for example, are destroyed by freeing their 'y'-field and then their 'x'-field.

The default destructor, however, does not always do a proper job. It is thus good practice to write an explicit destructor in the class block:

```
~point() {
} // destructor
```

Here, the actual destruction is done by the default destructor, which is invoked implicitly at the end of this destructor. This is why the body of this destructor is empty.

The default destructor, however, cannot properly destroy more complicated objects with data fields that are themselves pointers. Indeed, when the default destructor encounters such a field, it only destroys the address in it, not its content. The object in this address, although inaccessible because its address is no longer available, still occupies valuable memory. This is why an explicit destructor is required to delete this field properly using the reserved "delete" command. This command not only deletes the address in the field but also implicitly invokes the appropriate destructor to destroy the object in it and free the memory it occupies.

# 2.8 Member and Friend Functions

Interface functions may be of two possible kinds: member functions or friend functions. In what follows, we’ll describe the features of these kinds of functions.

Constructors, destructors, and assignment operators must be member functions. The above "X()", "Y()", and "zero" functions are also member functions: they are defined inside the class block and act upon the current object with which they are called. For example, the call "P.X()" applies the function "X()" to the "point" object 'P' and returns its 'x'-field, "P.x".

Since member functions are defined inside the class block, their definitions can use (or call) only other interface functions declared in the class block; they cannot use ordinary (noninterface) functions defined outside the class block unless they are declared friends of the class.

Member functions are called with a current object, e.g., 'P' in "P.X()". When a member function such as "X()" is executed, it is assumed that the fields 'x' and 'y' mentioned in its definition refer to the corresponding fields in the current object; 'x' is interpreted as "P.x", and 'y' is interpreted as "P.y".

Friend functions, on the other hand, have no current object and can only take arguments as in ordinary functions.