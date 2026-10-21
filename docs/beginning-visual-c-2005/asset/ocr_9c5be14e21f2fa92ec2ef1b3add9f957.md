# Chapter 8

It now has one argument that is the right operand for the / operator. The left operand is the current object referenced by the this pointer (implicitly in this case).

The operators are exercised in the four output statements. Only the last one is new to you and this combines the use of the overloaded + operator for Length objects with the overloaded / operator. The last argument to the Console::WriteLine() function in the fourth output statement is (len1+len2) / factor which is equivalent to the expression:

```
Length::operator/(len1.operator+(len2), factor).ToString()
```

The first argument to the static operator/() function is the Length object that is returned by the operator+() function, and the second argument is the factor variable, which is the divisor. The ToString() function for the Length object returned by operator/() is called to produce the argument string that is passed to the Console::WriteLine() function.

It is possible that you might want the capability to divide one Length object by another and have a value of type int as the result. This would allow you to figure out how many 17 inch lengths you can cut from a piece of timber 12 feet six inches long for instance. You can implement this quite easily like this:

```
static int operator/(Length len1, Length len2)
{
    return
    (len1.feet*inchesPerFoot + len1.inches) / ( len2.feet*inchesPerFoot + len2.inches);
}
```

This just returns the result of dividing the first length in inches by the second in inches.

To complete the set you could add a function to overload the % operator to tell you how much is left over. This could be implemented as:

```
static Length operator%(Length len1, Length len2)
{
    int ins = (len1.feet*inchesPerFoot + len1.inches) %
                (len2.feet*inchesPerFoot + len2.inches);
    return Length(ins/inchesPerFoot, ins%inchesPerFoot);
}
```

You compute the residue in inches after dividing len1 by len2 and return it as a new Length object.

With all these operators you really can use your Length objects in arithmetic expressions. You can write statements such as:

```
Length len1 = Length(2,6);        // 2 feet 6 inches
Length len2 = Length(3,5);        // 3 feet 5 inches
Length len3 = Length(14,6);       // 14 feet 6 inches
Length total = 12*(len1 + len2 + len3) + (len3/Length(1,7))*len2;
```

The value of total will be 275 feet 9 inches. The last statement makes use of the assignment operator that comes with every value class as well as the operator*(), operator+(), and operator/() functions in the Length class. This operator overloading is not only powerful stuff, it really is easy isn’t it?