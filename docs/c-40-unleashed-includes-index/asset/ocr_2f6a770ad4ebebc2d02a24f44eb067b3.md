```
case Color.Green:
    return "groen";
case Color.Blue:
    return "blauw";
}
```

Unfortunately, the preceding code doesn't compile because the C# compiler doesn't realize (for a good reason, read on) we're exhaustively testing for what appear to be all values in the domain of the Color enumeration. Because of this, it sees a code path exists that doesn't guarantee a string is returned from the method. Either we need to supply a default case or return some dummy value at the end of the method. Or we return in a forceful way by throwing an exception:

```
default:
    throw new InvalidOperationException("Unknown color.");
```

This can be particularly annoying if you're working on code coverage because it seems impossible to hit the default case. Wouldn't it be nice we could tell the compiler that switch is "complete" (or let it infer that)? It would, if enumeration types would really establish finite domains. But they don't.

You already know this from one use of enumerations, with flags. In Chapter 5, we looked at bit-level mask operations to test for flags. An enumeration for FileMode can have Read and Write values defined as powers of two, allowing the user to combine them into a ReadWrite by using the bitwise | operator. We've just created a value that's also a valid FileMode but hasn't necessarily been declared explicitly in the enumeration.

But also without the use of flags, enumerations are just integral numbers in disguise. In our Color definition, the enumeration is really an int with some symbolic constants defined using compiler-generated numbers (Red = 0, Green = 1, and Blue = 2). Because the integral representation is handy as a storage mechanism (as opposed to storing a new as a string), you can convert back and forth between an enumeration and its underlying type:

```
var unknownColor = (Color)4;
```

Here's how an unknown enumeration value can be born, a little unfortunately.

From a stylistic point of view, an often-recurring question is whether a switch statement's embedded statements should be wrapped in a pair of curly braces. Remember, blocks can be used for scoping purposes, so the use of curly braces can be beneficial in case you need local state and don't want to spoil the outer scope:

```
static int Eval(Expression ex)
{
    switch (ex.NodeType)
    {
```