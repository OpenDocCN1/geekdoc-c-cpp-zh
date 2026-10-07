# Chapter 23: Platform Interoperability and Unsafe Code

dereference the address using the indirection operator and then assign the location with a different character. Similarly, using the + and - operators on a pointer changes the address by the * sizeof(T) operand, where T is the referent type.

The comparison operators (==, !=, <, <=, and >=) also work to compare pointers. Thus, their use effectively translates to a comparison of address values.

One restriction on the dereferencing operator is the inability to dereference a void*. The void* data type represents a pointer to an unknown type. Since the data type is unknown, it can't be dereferenced to produce a variable. Instead, to access the data referenced by a void*, you must convert it to another pointer type and then dereference the latter type.

You can achieve the same behavior as implemented in Listing 23.17 by using the index operator rather than the indirection operator (see Listing 23.18 with Output 23.4).

# LISTING 23.18: Modifying an Immutable String with the Index Operator in Unsafe Code

```
string text = "S5280ft";
Console.Write("{0} = \ text);
safe // Requires /unsafe switch
fixed(char* pText)
{
    pText[1] = 'm';
npText[2] = 'i';
pText[3] = 'l';
pText[4] = 'e';
pText[5] = 'f';
npText[6] = 't';
}
Console.WriteLine(text);
```

# OUTPUT 23.4

S5280ft = Smile

Modifications such as those in Listing 23.17 and Listing 23.18 can lead to unexpected behavior. For example, if you reassigned text to "S5280ft",