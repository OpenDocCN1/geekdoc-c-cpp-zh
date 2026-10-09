you must convert it to any other pointer type and then dereference the later type.

You can achieve the same behavior as implemented in Listing 21.17 by using the index operator rather than the indirection operator (see Listing 21.18).

# **LISTING 21.18: Modifying an Immutable String with the Index Operator in Unsafe Code**

```
string text;
text = "S$280ft";
Console.Write("{0} = ", text);

unsafe // Requires /unsafe switch
{
  fixed (char* pText = text)
  {
    pText[1] = 'm';
    pText[2] = 'i';
    pText[3] = 'l';
    pText[4] = 'e';
    pText[5] = ' ';
    pText[6] = ' ';
  }
}
Console.WriteLine(text);
```

The results of Listing 21.18 appear in Output 21.4.

# **OUTPUT 21.4**

> S$280ft = Smile

Modifications such as those in Listing 21.17 and Listing 21.18 can lead to unexpected behavior. For example, if you reassigned text to "S$280ft" following the Console.WriteLine() statement and then redisplayed text, the output would still be Smile because the address of two equal string literals is optimized to one string literal referenced by both variables. In spite of the apparent assignment

```
text = "S$280ft";
```

after the unsafe code in Listing 21.17, the internals of the string assignment are an address assignment of the modified "S$280ft" location, so text is never set to the intended value.