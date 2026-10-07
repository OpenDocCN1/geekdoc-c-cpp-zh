# Pointers and Addresses

following the Console.WriteLine() statement and then redisplayed text, the output would be Smile because the address of two equal string literals is optimized to one string literal referenced by both variables. In spite of the apparent assignment

text = "S5280ft";

after the unsafe code in Listing 23.17, the internals of the string assignment are an address assignment of the modified "S5280ft" location, so text is never set to the intended value.

# Accessing the Member of a Referent Type

Derefencing a pointer produces a variable of the pointer's underlying type. You can then access the members of the underlying type using the member dot operator in the usual way. However, the rules of operator precedence require that *x.y means (*x).y, which is probably not what you intended. If x is a pointer, the correct code is (*).y, which is an unpleasant syntax. To make it easier to access members of a dereferenced pointer, C# provides a special member access operator: x->y is a shorthand for (*x).y, as shown in Listing 23.19 with Output 23.5.

# LISTING 23.19: Accessing a Referent Type's Members

```
unsafe{
    Angle angle = new(30, 18, 0);
    Angle*pAngle = &angle;
    System.Console.WriteLine("{0} {1} {2}",
    pAngle->Hours, pAngle->Minutes, pAngle->Seconds);
}
```

# OUTPUT 23.5

30° 18' 0