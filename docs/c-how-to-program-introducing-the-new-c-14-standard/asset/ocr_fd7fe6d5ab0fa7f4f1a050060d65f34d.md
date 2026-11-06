# 21.2 `string` Assignment and
Concatenation

**Figure 21.1** demonstrates `string` *assignment and concatenation*. Line 4 includes header `<string>` for class `string`. The strings `string1`, `string2` and `string3` are created in lines 8–10. Line 12 assigns the value of `string1` to `string2`. After the assignment takes place, `string2` is a copy of `string1`. Line 13 uses member function `assign` to copy `string1` into `string3`. A separate copy is made (i.e., `string1` and `string3` are independent objects). Class `string` also provides an overloaded version of member function `assign` that copies a specified number of characters, as in

```
targetString.assign(sourceString, start, numberOfCharacters);
```

where `sourceString` is the `string` to be copied, `start` is the starting subscript and `numberOfCharacters` is the number of characters to copy.