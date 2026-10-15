# Length

You can obtain the length of an array, as shown in Listing 2.48.

```
Console.WriteLine(
    $"There are { languages.Length } languages in the array.");
```

Arrays have a fixed length; they are bound such that the length cannot be changed without re-creating the array. Furthermore, overstepping the bounds (or length) of the array will cause the runtime to report an error. This can occur when you attempt to access (either retrieve or assign) the array with an index for which no element exists in the array. Such an error frequently occurs when you use the array length as an index into the array, as shown in Listing 2.49.

```
string languages = new string[9];
...
// RUNTIME ERROR: index out of bounds - should
// be 8 for the last element
languages[4] = languages[9];
```

> **NOTE**
> 
> The Length member returns the number of items in the array, not the highest index. The Length member for the languages variable is 9, but the highest index for the languages variable is 8, because that is how far it is from the start.

It is a good practice to use Length in place of the hardcoded array size. To use Length as an index, for example, it is necessary to subtract 1 to avoid an out-of-bounds error (see Listing 2.50).

```
string languages = new string[9];
...
languages[4] = languages[languages.Length - 1];
```