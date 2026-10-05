# Basic Operator Overloading

The values of m3 and (m1 + m2) are two different objects. The assignment operator does not make m3 the same as the (m1 + m2). Instead, it copies the values of the member variables of (m1 + m2) into the member variables of m3. With objects of a class, the default assignment operator does not make the two objects same object, it only copies values of member variables from one object to another.

This distinction is subtle but important. It may help you understand the details if you recall that a variable of a class and an object of a class type are not the same thing. An object is a value of a class type and may be stored in a variable of a class type, but the variable and the object are not the same thing. In the code

```
m3 = (m1 + m2);
```

the variable m3 and its value (m1 + m2) are different things, just as n and 5 are different things in

```
int n = 5;
```

or in

```
int n = (2 + 3);
```

It may take a while to become comfortable with this notion of return by const value. In the meantime, a general rule of thumb is to always return by const value unless you have an explicit reason to do so. For most simple programs this will have no effect on your program than to flag such subtle errors.
Note that although it is legal, it is pointless to return base types, such as int, or const value. The const has no effect in basic cases. When a function or returns a value of one of the basic types, such as int, double, or char, it returns the value, such as 5, 5.5, or 'A'. It does not return a variable or anything like a variable. Unlike unlike, the value cannot be changed—you cannot change 5. Values of a basic type cannot be changed whether there is a const before the return type or not. On the other hand, values of a class type—that is, objects—can be changed, since they have member variables, and so the const modifier has an effect on the object returned.

# Self-Test Exercise

+   4. You omit the const at the beginning of the declaration and definition of the overloaded operator for the class Money, so that the value is not returned by const value. Is this the legal?

```
Money(10.99), m2(23.57), m3(12.34);
(m1 + m2) = m3;
```

Is it legal if the definition of the class Money is as shown in Display 8.1, so that the plus operator returns its value by const value?

![](bbox=[0.05, 0.706, 0.178, 0.732])