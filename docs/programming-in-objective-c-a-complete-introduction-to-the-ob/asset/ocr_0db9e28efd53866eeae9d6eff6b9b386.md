# Chapter 13 Underlying C Language Features

In the main routine, the copyString function is called twice—the first time to copy the contents of string1 into string2, and the second time to copy the contents of the constant string "So is this." into string2.

# Constant Strings and Pointers

The fact that the call

```
copyString(string2, "So is this.");
```

works in the previous program implies that when a constant string is passed as an argument to a function, that character is actually passed to a pointer. Not only is this true in this case, but it can be generalized by saying that whenever a constant string is used in Objective-C, a pointer to that character string is produced.

This point might sound a bit confusing now, but as we briefly noted in Chapter 4, constant character strings that we mention here are C-style strings. These are not objects. As you know, a constant string object is created by putting an @ sign in front of the string, as @"This is okay."You cannot substitute one for the other.

If textPtr is declared to be a character pointer, as in

```
char textPtr;
```

then the statement

```
textPtr = "A character string.";
```

assigns to textPtr a pointer to the constant character string "A character string." Be careful to make the distinction between character pointers and character arrays because the type of assignment previously is not valid with a character array. For example, if text were defined instead to be an array of chars, with a statement such as

```
char text[80];
```

you could not write a statement such as this:

```
text = "This is not valid.";
```

The only time Objective-C lets you get away with performing this type of assignment to a character array when initializing it:

```
char text[80] = "This is okay.";
```

> ² Note the use of the strings "A string to be copied." and "So is this." in the program. These are not string objects, but C-style character strings, as distinguished by the fact that an @ character does not precede the string. The two types are not interchangeable. If a function expects an array of chars as an argument, you may pass it either an array of type char or a literal C-style string, but not a character string object.