In this case, you take the original address and increment it by the size of the referent type (sizeof(char)), using the preincrement operator. Next, you dereference the address using the indirection operator and then assign the location with a different character. Similarly, using the + and - operators on a pointer changes the address by the * sizeof(T) operand, where T is the referent type.

Similarly, the comparison operators (==, !=, <, >, <=, and >=) work to compare pointers translating effectively to the comparison of address location values.

One restriction on the dereferencing operator is the inability to dereference a void*. The void* data type represents a pointer to an unknown type. Since the data type is unknown, it can't be dereferenced to another type. Instead, to access the data referenced by a void*, you must convert it to any other pointer type variable and then dereference the latter type, for example.

You can achieve the same behavior as Listing 20.17 by using the index operator rather than the indirection operator (see Listing 20.18).

# LISTING 20.18: Modifying an Immutable with the Index Operator in Unsafe Code

```
string text;
text = "55280ft";
Console.Write("({0} = ", text);
Unsafe // Requires /unsafe switch.
{
    fixed (char* pText = text)
    {
        pText[1] = 'm';
        pText[2] = 'i';
        pText[3] = 'l';
        pText[4] = 'e';
        pText[5] = 's';
        pText[6] = ' ';
    }
}
Console.WriteLine(text);
```

The results of Listing 20.18 appear in Output 20.3.

# OUTPUT 20.3:

```
55280ft = Smile
```