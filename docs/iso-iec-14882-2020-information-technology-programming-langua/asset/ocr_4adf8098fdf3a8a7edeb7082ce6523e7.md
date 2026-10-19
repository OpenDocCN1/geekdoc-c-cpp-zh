```
void f ();
};

A a;

void B::f() {
    operator+ (a,a);        // error: global operator hidden by member
    a + a;                  // OK: calls global operator+
}
```

— end note]

# 12.4.2.4 Initialization by constructor [over.match.ctor]

1 When objects of class type are direct-initialized (9.4), copy-initialized from an expression of the same or a derived class type (9.4), or default-initialized (9.4), overload resolution selects the constructor. For direct-initialization or default-initialization that is not in the context of copy-initialization, the candidate functions are all the constructors of the class of the object being initialized. For copy-initialization (including default initialization in the context of copy-initialization), the candidate functions are all the converting constructors (11.4.8.2) of that class. The argument list is the expression-list or assignment-expression of the initializer.

# 12.4.2.5 Copy-initialization of class by user-defined conversion [over.match.copy]

1 Under the conditions specified in 9.4, as part of a copy-initialization of an object of class type, a user-defined conversion can be invoked to convert an initializer expression to the type of the object being initialized. Overload resolution is used to select the user-defined conversion to be invoked.

> [Note 1: The conversion performed for indirect binding to a reference to a possibly cv-qualified class type is determined in terms of a corresponding non-reference copy-initialization. — end note]

Assuming that “cv1 T” is the type of the object being initialized, with T a class type, the candidate functions are selected as follows:

+   (1.1) — The converting constructors (11.4.8.2) of T are candidate functions.

+   (1.2) — When the type of the initializer expression is a class type “cv S”, the non-explicit conversion functions of S and its base classes are considered. When initializing a temporary object (11.4) to be bound to the first parameter of a constructor where the parameter is of type “reference to cv2 T” and the constructor is called with a single argument in the context of direct-initialization of an object of type “cv3 T”, explicit conversion functions are also considered. Those that are not hidden within S and yield a type whose cv-unqualified version is the same type as T or is a derived class thereof are candidate functions. A call to a conversion function returning “reference to X” is a glvalue of type X, and such a conversion function is therefore considered to yield X for this process of selecting candidate functions.

2 In both cases, the argument list has one argument, which is the initializer expression.

> [Note 2: This argument will be compared against the first parameter of the constructors and against the implicit object parameter of the conversion functions. — end note]

# 12.4.2.6 Initialization by conversion function [over.match.conv]

1 Under the conditions specified in 9.4, as part of an initialization of an object of non-class type, a conversion function can be invoked to convert an initializer expression of class type to the type of the object being initialized. Overload resolution is used to select the conversion function to be invoked. Assuming that “cv1 T” is the type of the object being initialized, and “cv S” is the type of the initializer expression, with S a class type, the candidate functions are selected as follows:

+   (1.1) — The conversion functions of S and its base classes are considered. Those non-explicit conversion functions that are not hidden within S and yield type T or a type that can be converted to type T via a standard conversion sequence (12.4.4.2.2) are candidate functions. For direct-initialization, those explicit conversion functions that are not hidden within S and yield type T or a type that can be converted to type T with a qualification conversion (7.3.6) are also candidate functions. Conversion functions that return a cv-qualified type are considered to yield the cv-unqualified version of that type for this process of selecting candidate functions. A call to a conversion function returning “reference to X” is a glvalue of type X, and such a conversion function is therefore considered to yield X for this process of selecting candidate functions.