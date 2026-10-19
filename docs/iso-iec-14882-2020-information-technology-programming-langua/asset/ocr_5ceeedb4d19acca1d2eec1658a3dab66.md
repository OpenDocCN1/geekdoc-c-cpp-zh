— end example]
— end note]
—— Otherwise, the initialization is ill-formed.

—— Otherwise (i.e., for the remaining copy-initialization cases), user-defined conversions that can convert from the source type to the destination type or (when a conversion function is used) to a derived class thereof are enumerated as described in 12.4.2.5, and the best one is chosen through overload resolution (12.4). If the conversion cannot be done or is ambiguous, the initialization is ill-formed. The function selected is called with the initializer expression as its argument; if the function is a constructor, the call is a prvalue of the cv-unqualified version of the destination type whose result object is initialized by the constructor. The call is used to direct-initialize, according to the rules above, the object that is the destination of the copy-initialization.

—— Otherwise, if the source type is a (possibly cv-qualified) class type, conversion functions are considered. The applicable conversion functions are enumerated (12.4.2.6), and the best one is chosen through overload resolution (12.4). The user-defined conversion so selected is called to convert the initializer expression into the object being initialized. If the conversion cannot be done or is ambiguous, the initialization is ill-formed.

—— Otherwise, if the initialization is direct-initialization, the source type is std::nullptr_t, and the destination type is bool, the initial value of the object being initialized is false.

—— Otherwise, the initial value of the object being initialized is the (possibly converted) value of the initializer expression. A standard conversion sequence (7.3) will be used, if necessary, to convert the initializer expression to the cv-unqualified version of the destination type; no user-defined conversions are considered. If the conversion cannot be done, the initialization is ill-formed. When initializing a bit-field with a value that it cannot represent, the resulting value of the bit-field is implementation-defined.

> [Note 8: An expression of type “cv1 T” can initialize an object of type “cv2 T” independently of the cv-qualifiers cv1 and cv2.

```
int a;
const int b = a;
int c = b;
```

— end note]

18 An initializer-clause followed by an ellipsis is a pack expansion (13.7.4).

19 If the initializer is a parenthesized expression-list, the expressions are evaluated in the order specified for function calls (7.6.1.3).

20 The same identifier shall not appear in multiple designators of a designated-initializer-list.

21 An object whose initialization has completed is deemed to be constructed, even if the object is of non-class type or no constructor of the object’s class is invoked for the initialization.

> [Note 9: Such an object can use value-initializion, aggregate initialization (9.4.2), or initialization by an inherited constructor (11.10.4). — end note]

Destroying an object of class type invokes the destructor of the class. Destroying a scalar type has no effect other than ending the lifetime of the object (6.7.3). Destroying an array destroys each element in reverse subscript order.

22 A declaration that specifies the initialization of a variable, whether from an explicit initializer or by default-initialization, is called the initializing declaration of that variable.

> [Note 10: In most cases this is the defining declaration (6.2) of the variable, but the initializing declaration of a non-inline static data member (11.4.9.3) can be the declaration within the class definition and not the definition at namespace scope. — end note]

# 9.4.2 Aggregates

1 An aggregate is an array or a class (Clause 11) with

+   —— no user-declared or inherited constructors (11.4.5),

+   —— no private or protected direct non-static data members (11.9),

+   —— no virtual functions (11.7.3), and

+   —— no virtual, private, or protected base classes (11.7.2).