# A.2.13 <see>

This tag allows a link to be specified within text. Use <seealso> (§A.2.14) to indicate text that is to appear in a See Also section.

# Syntax:

```
<see cref="member"/>
```

where

```
cref="member"
```

The name of a member. The documentation generator checks that the given code element exists and changes member to the element name in the generated documentation file.

# Example:

```
/// <summary>This method changes the point's location to
/// the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

# A.2.14 <seealso>

This tag allows an entry to be generated for the See Also section. Use <see> (§A.2.13) to specify a link from within text.

# Syntax:

```
<seealso cref="member"/>
```

where

```
cref="member"
```

The name of a member. The documentation generator checks that the given code element exists and changes member to the element name in the generated documentation file.