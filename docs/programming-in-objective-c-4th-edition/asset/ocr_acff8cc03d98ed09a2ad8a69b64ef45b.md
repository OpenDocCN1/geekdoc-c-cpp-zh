Program 15.3 first declares three immutable NSString objects: strl, str2, and res. The first two are initialized to constant character string objects. The declaration

```
NSComparisonResult compareResult;
```

declares compareResult to hold the result of the string comparison that will be performed later in the program.

You can use the length method to count the number of characters in a string. It returns an unsigned integer value of type NSInteger. The output verifies that the string

contains 16 characters. The statement

```
res = [NSString stringWithString:strl];
```

shows how to create a new character string with the contents of another. The resulting NSString object is assigned to res and is then displayed to verify the results. An actual copy of the string contents is made here, not just another reference to the same string in memory. That means that strl and res refer to two different string objects, which is different than simply performing a simple assignment like this:

```
res = strl;
```

As we have previously discussed, this statement would simply create another reference to the same object in memory.

The stringByAppendingString: method can join two character strings. So the expression

```
[strl stringByAppendingString: str2]
```