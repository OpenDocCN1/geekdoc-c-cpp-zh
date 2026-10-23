
Here, the interface functions are only declared in the class block, while their actual definitions are left outside it. Each definition is compiled only once, which creates a finite state machine (automaton). This machine is then invoked every time the function is called, with the concrete arguments that are passed to the function as input and the returned value as output.

The prefix "point::" that precedes the function names in the above code may actually be considered as an operator that “transfers” the definition back into the class block. This format, however, is unnecessary in the present “point” example, which uses very short definitions. The original style, in which the complete definitions appear inside the class block, is preferable in this case.

```cpp
void point::zero(){
    x=y=0.;
}   // definition of "zero()"
```

### 2.3 Constructors

When the user defines a point object by writing

```cpp
point P;
```

the computer executes this command by allocating memory for the data fields of the new "point" variable 'P'. These data fields, the "double" variables "P.x" and "P.y", are not yet initialized to any meaningful value; in fact, they initially contain random, meaningless values. Only interface functions of the "point" class have access to these variables and can assign meaningful values to them.

C++ has a default constructor that allocates memory for the data fields and initializes them with random values. However, this is not always good enough. Programmer A might have a different idea about what should happen when the user writes code lines like "point P;", and he/she might also want users to be able to write more sophisticated code lines like "point P = 0;", in which 'P' is constructed and initialized to zero. Indeed, if the "point" object is to behave like standard types, then such commands should be available to users.

It is thus good practice to write an explicit constructor in the class. The constructor is a public interface function that tells the computer how to construct a new object and allocate memory for its data fields. The name of the constructor function must be the same as the name of the class itself. For example, if one writes in the block of the "point" class

```cpp
point(){
}   // default constructor for the "point" class
```

then this constructor is invoked every time the compiler encounters a command of the form "point P;". The body of the constructor function contains no code lines at all. However, it still does something: as soon as it is called, the constructor implicitly invokes the default constructor built into C++, which allocates storage for the data fields "P.x" and "P.y" and fills them with random numbers. The above constructor is also called the default constructor for the "point" class, because it is invoked by commands like "point P;", with no initialization at all.

It is possible to write more than one constructor in the class block. In particular, one may also define a more informative constructor, which not only allocates memory for the data fields in the constructed object but also initializes them with meaningful values. For example, if one writes in the block of the "point" class

```cpp
point(double xx,double yy){
    x=xx;
    y=yy;
}
```

then this constructor is invoked every time the compiler encounters a command of the form

```cpp
point P(3.,5.);
```

to create a new "point" object 'P' with the value 3 in its 'x'-field and the value 5 in its 'y'-field.

Here is how this constructor works. When it is called, it first implicitly invokes the default constructor built into the C++ compiler, which allocates memory to the 'x'- and 'y'-fields and fills them with random numbers. Then, the 'x'- and 'y'-fields are reassigned their correct values from the corresponding arguments "xx" and "yy", respectively.

This process is somewhat inefficient. Why not initialize the 'x'- and 'y'-fields immediately with their correct values? This can indeed be done by using an initialization list as follows:

```cpp
point(double xx,double yy):x(xx),y(yy){
} // constructor with initialization list
```

The initialization list that follows the character ':' is a list of data fields in the constructed object, separated by commas. Each data field is followed by its initial value in parentheses. When this constructor is called, the fields are allocated memory and initialized properly in the order in which they appear (are declared) in the class block, and not necessarily in the order in the initialization list. The construction and initialization are then complete, so there is nothing left to do in the function block, and it remains empty.

Better yet, one may rewrite the above constructor as follows:

```cpp
point(double xx=0.,double yy=0.):x(xx),y(yy){
} // arguments with default values
```

This way, the arguments "xx" and "yy" take the default value 0, which is used whenever they are not specified explicitly. This constructor also serves as a default constructor in the "point" class, so there is no need to write any other constructor. When the compiler encounters commands like

```cpp
point P(3.,5.);
point Q(3.); // or point Q=3.;
point W;
```

it completes the missing arguments with zeroes and constructs three point objects: 'P' with 'x'-field initialized to 3 and 'y'-field initialized to 5, 'Q' with 'x'-field initialized to 3 and 'y'-field initialized to 0 (because the second argument "yy" is not specified and therefore takes the default value 0), and 'W' with both fields initialized to 0 (because both arguments "xx" and "yy" are unspecified).

### 2.4 Explicit Conversion

The above constructor also provides an explicit conversion operator from type "double" to type "point". As in C, where "(double)n" produces a temporary "double" variable with the same value as the integer variable 'n', "(point)a" produces a temporary "point" object whose first field contains the same value as the "double" variable 'a' and whose second field is zero. This is done by invoking the above constructor, with 'a' serving as the first argument and no second argument. Thanks to the default values in the above code, the second argument implicitly takes the zero value, which is then assigned to the second field in the temporary variable returned by the "(point)" function. This is called explicit conversion.

The term “conversion” is somewhat confusing. Actually, 'a' is never converted or changed in any way. It is only used as an argument for the "(point)" function. In fact, one can write equivalently "point(a)" and obtain the same result: a temporary "point" object with first field equal to 'a' and second field zero. This object can be used only in the very code line in which it was constructed and disappears soon after. Although the term “conversion” is inaccurate, it is convenient and commonly used to refer to this function.

### 2.5 Implicit Conversion

The above constructor also provides implicit conversion from type "double" to type "point". In code where a variable of type "point" is expected and a variable of type "double" appears instead, the above constructor is invoked implicitly to convert the "double" variable into the required "point" variable. This feature may be particularly useful in functions that take "point" arguments. When such a function is called with a "double" argument, it is converted implicitly into the required "point" argument. This feature is analogous to type conversion in C. On one hand, it may make codes more transparent and straightforward; on the other hand, it may also be too expensive, as we'll see below.

Implicit conversion requires an extra call to the constructor. The memory allocation in this construction requires extra computer time to complete. Although this overhead may be negligible for small objects such as points, it may be significant for larger objects, particularly if the implicit conversion is repeated many times in long loops. One should thus consider carefully whether or not to use implicit conversion.

### 2.6 The Default Copy Constructor

The above constructor can be used to construct new "point" objects and initialize them with prescribed values. However, users of the "point" class should also be able to use existing objects to initialize new ones. For example, they would surely like to write code such as

```cpp
point P(3.,5.);
point Q(P); // or point Q=P;
```

where 'P' is first constructed as before, and then 'Q' is constructed and initialized to have the same value as 'P'. This is done by the copy constructor.

The copy constructor constructs (allocates memory for) a new object and initializes it with the value of the object passed to it as an argument. The construction and initialization
