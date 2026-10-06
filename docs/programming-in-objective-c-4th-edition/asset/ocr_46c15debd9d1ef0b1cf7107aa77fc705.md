Figure 15.4.

# Figure 15.4. Indexing into a string

![](bbox=[0.187, 0.211, 0.812, 0.307])

The rangeOfString: method is used in the lines that follow in Program 15.5 to show how a string can first be located and then deleted. After first verifying that @“string B and” does not exist in mstr, the deleteCharactersInRange: method is used to delete the characters, using the range returned from the range: method as its argument.

You can use the set: method to directly set the contents of a mutable string object. After using this method to set mstr to the string @“This is string A”, the replaceCharactersInRange:withString: method replaces some of the characters in the string with another string. The sizes of the strings do not have to be the same; you can replace one string with another of equal or unequal sizes. So in the statement

```
[mstr replaceCharactersInRange: NSNameRange(8, 8)
withString: @"a mutable string"];
```

the 8 characters “string A” are replaced with the 16 characters “a mutable string”.

The remaining lines in the program example show how to perform search and replace operations. In the first case, you locate the string @“This is” inside the string mstr, which has been set to @“This