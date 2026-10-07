```
entryNumber = lookup (dictionary, argv[1], entries);
```

```
return (0);
}
```

The main routine tests execute to ensure that a word was typed after the program name when the program was executed. If it wasn't, or if more than one word was typed, the value of argc is not equal to 2. In this case, the program writes an error message to standard error and terminates, returning an exit status of 1.

If argc is equal to 2, the lookup function is called to find the word argv[1] points to the dictionary. If the word is found, its definition is displayed.
Remember command-line arguments are always stored as character strings. So execution of the program power with the command-line arguments 2 and 16, as

power 16

stores a pointer to the character string "2" inside argv[1] and a pointer to the string "16" inside argv[2]. If the program is to interpret arguments as numbers (we suspect is in the case of the program), the itself must convert them. Several routines are available in the program library for doing conversions: scanf, atof, atoi, strtok and strtol. In Part II, you will learn how to use a class NSProcessInfo to access the command-line arguments as string objects instead of C strings.

# How Things Work

We would remiss if we finished this chapter without first tying a couple together. Because the Objective-C language has the C language underneath, it's worth mentioning some of the connections between the two. You can implement details or use them to better understand how things works, in the way that learning about objects as memory addresses can help you understand pointers. We don't get too detailed here; we just state four facts about the relationship between Objective-C and C.

# Fact #1: Instance Variables areored in Structures

When you define a class and its instance variables, those instance variables are actually stored inside a structure.That's how you can manipulate objects; they're really structures variables. So the inherited instance variables plus the ones you added in your class comprise a single structure.When you allocate a new object using alloc, enough space is reserved to hold one of these structures.