the constructor with a `String` parameter. If that constructor throws an exception, the edit is not valid. You can try that out in the example program by entering a URL that does not start with a prefix such as `http:`.

> > **NOTE:** By default, the `DefaultFormatter` is in *overwrite mode*. That is different from the other formatters and not very useful. Call `setOverwriteMode(false)` to turn off overwrite mode.

Finally, the `MaskFormatter` is useful for fixed-size patterns that contain some constant and some variable characters. For example, Social Security numbers (such as 078-05-1120) can be formatted with a

```
```
new MaskFormatter("##-##-####")
```
```

The `#` symbol denotes a single digit. Table 10.3 shows the symbols that you can use in a mask formatter.

# **Table 10.3** MaskFormatter Symbols

| Symbol | Explanation |
| --- | --- |
| `#` | A digit |
| `?` | A letter |
| `U` | A letter, converted to upper case |
| `L` | A letter, converted to lower case |
| `A` | A letter or digit |
| `H` | A hexadecimal digit (`[0-9a-fA-F]`) |
| `*` | Any character |
| `'` | Escape character to include a symbol in the pattern |

You can restrict the characters that can be typed into the field by calling one of the methods of the `MaskFormatter` class:

```
```
setValidCharacters
setInvalidCharacters
```
```

For example, to read in a letter grade (such as `A+` or `F`), you could use

```
```
MaskFormatter formatter = new MaskFormatter("U*");
formatter.setValidCharacters("ABCDF+- ");
```
```

However, there is no way of specifying that the second character cannot be a letter.