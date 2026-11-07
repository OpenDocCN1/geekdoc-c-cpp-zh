But if you really need a conversion, it allows the following:

```
int plb = poppins.Stone_to_Int();
```

> **Caution**
> 
> You should use implicit conversion functions with care. Often a function that can only be invoked explicitly is the best choice.

In summary, then, C++ provides the following type conversions for classes:

+   - A class constructor that has but a single argument serves as an instruction for converting a value of the argument type to the class type. For example, the Stonewt class constructor with a type int argument is invoked automatically when you assign a type int value to a Stonewt object. However, using `explicit` in the constructor declaration eliminates implicit conversions and allows only explicit conversions.
+   - A special class member operator function called a *conversion function* serves as an instruction for converting a class object to some other type. The conversion function is a class member, has no declared return type, has no arguments, and is called operator `typeName()`, where `typeName` is the type to which the object is to be converted. This conversion function is invoked automatically when you assign a class object to a variable of that type or use the type cast operator to that type.

# Conversions and Friends

Let’s bring addition to the Stonewt class. As mentioned in the discussion of the Time class, you can use either a member function or a friend function to overload addition. (To simplify matters, assume that no conversion functions of the operator double() form are defined.) You can implement addition with the following member function:

```
Stonewt Stonewt::operator+(const Stonewt & st) const
{
    double pds = pounds + st.pounds;
    Stonewt sum(pds);
    return sum;
}
```

Or you can implement addition as a friend function this way:

```
Stonewt operator+(const Stonewt & st1, const Stonewt & st2)
{
    double pds = st1.pounds + st2.pounds;
    Stonewt sum(pds);
    return sum;
}
```

Remember, you can provide the method definition or the friend definition but not both. Either form lets you do the following: