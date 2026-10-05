
# 354 CHAPTER 8 Operator Overloading, Friends, and References 

> TIP: (continued)

The following summary may be of help. T is assumed to be a class type.

- Simple returning by value, as in the function declaration T f(); Cannot be used as an l-value, and the returned value can be changed directly as in f().mutator(). Calls the constructor.
- Returning by constant value, as in const T f(); This is the same as the previous case, but the returned value cannot be changed directly as in f().mutator().
- Returning by reference as in T& f(); Can be used as an l-value, and the returned value can be changed directly as in f().mutator(). Does not call the constructor.
- Returning by constant reference, as in const T& f(); Cannot be used as an l-value, and the returned value cannot be changed directly as in f().mutator(). Does not call the constructor.

## Overloading >> and <<

The input and output operators >> and << can be overloaded just like any other operators. If you want the operators to behave as expected for cin, cout, and file I/O, then the value returned should be of type istream for input and ostream for output, and the value returned by reference.

## DECLARATIONS

```cpp
class Class_Name {
    ...
public:
    friend istream& operator >>(istream& Parameter_1,
                               Class_Name& Parameter_2);
    friend ostream& operator <<(ostream& Parameter_3,
                               const Class_Name& Parameter_4);
    ...
```

The operators do not need to be friends but cannot be members of the class being input or output.

## References and More Overloaded Operators

## DEFINITIONS

```cpp
iostream& operator >>(istream& Parameter_1,
    Class_Name& Parameter_2)
{
    ...
}
ostream& operator << (ostream& Parameter_3,
    const Class_Name& Parameter_4)
{
    ...
}
```

If you have enough accessor and mutator functions, you can overload >> and << as nonfriend functions. However, it is natural and more efficient to define them as friends.

## The Assignment Operator

If you overload the assignment operator =, you must overload it as a member operator. If you do not overload the assignment operator =, then you automatically get an assignment operator for your class. This default assignment operator copies the values of member variables from one object of the class to the corresponding member variables of another object of the class. For simple classes, that is usually what you want. When we discuss pointers, this default assignment operator will not be what we want, and we will discuss overloading the assignment operator at that point.

## Overloading the Increment and Decrement Operators

The increment and decrement operators ++ and -- each have two versions. They can do different things depending on whether they are used in prefix notation, ++x, or postfix (suffix) notation, x++. Thus, when overloading these operators, you need to distinguish between prefix and postfix versions so that you can have two versions of overloaded operator. In C++ this distinction between prefix and postfix versions is handled in a way that first reading (and maybe even on reading) seems a bit contrived. If you overload the ++ operator in the regular way (as a member with one parameter or as a member with no parameters), you have overloaded the prefix form. To obtain the postfix version, x++ or x--, you add a second parameter of type int. This is just a marker for the compiler; you do not need a second argument when you invoke x++ or x--.

For example, Display 8.6 contains the definition of a class whose data is pairs of integers. The increment operator works in both prefix and postfix notation. We have defined ++ so that it has the intuitive spirit of ++ on int variables. This is the best way to define ++, but you are free to return it any kind of type and perform any kind of action.

prefix
postfix

# 356 CHAPTER 8 Operator Overloading, Friends, and References

The definition of the postfix version ignores int parameter, as shown in Display 8.6. When the compiler sees ++, it treats it as an invocation of IntPair::operator++(int), with as the calling object.

The increment and decrement operator on simple types, as int and char, return by reference in the prefix form and by value in the postfix form. If you want to emulate what happens with simple types when you overload these operators for your class, then you would return by reference for the prefix form and by value for the postfix form.

(Note: The remaining text in the OCR appears to be heavily jumbled/corrupted with overlapping pages and fragments, but the logical flow follows the headers provided above.)
