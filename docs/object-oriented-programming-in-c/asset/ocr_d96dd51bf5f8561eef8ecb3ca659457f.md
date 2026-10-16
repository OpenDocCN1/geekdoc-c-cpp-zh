Following is the output of Program 7.5:

```
Product details-invent1 type
Code: 100
Items: 5
Value: 140
Stock value
Value = 700
Product details-invent2 type
Code: 100
Value: 700
```

# note

We have used the conversion function

```
operator float( )
```

in the class **invent1** to convert the **invent1** type data to a **float**. The constructor

```
invent2 (invent1)
```

is used in the class **invent2** to convert the **invent1** type data to the **invent2** type data.

Remember that we can also use the casting operator function

```
operator invent2()
```

in the class invent1 to convert **invent1** type to **invent2** type. However, it is important that we do not use both the constructor and the casting operator for the same type conversion, since this introduces an ambiguity as to how the conversion should be performed.

# SUMMARY

+   ↔ Operator overloading is one of the important features of C++ language. It is called compile time polymorphism.
+   ↔ Using overloading feature we can add two user defined data types such as objects, with the same syntax, just as basic data types.
+   ↔ We can overload almost all the C++ operators except the following:
+     • class member access operators(., .*)
+     • scope resolution operator (::)