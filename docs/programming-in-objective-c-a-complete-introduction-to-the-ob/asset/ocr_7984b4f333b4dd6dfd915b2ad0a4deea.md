Chapter 10 More on Variables and Data Types

# Program 10.3  Output

Enter month:
5

Number of days is 31

# Program 10.3  Output (Rerun)

Enter month:
2
Number of days is 28
or 29 if it's a leap year

You can explicitly assign an integer value to an enumerated data type variable; you should do this using the type cast operator. Therefore, if monthValue were an integer variable that had the value 6, for example, this would be permissible:

```
lastMonth = (enum month)(monthValue - 1);
```

If you don't use the type cast operator, the compiler (unfortunately) will complain about it.

When using programs with enumerated types, try not to rely on the fact that the enumerated values are treated as integers. Instead, treat them as distinct data types. The enumerated data type gives you a way to associate a symbolic name with an integer number. If you subsequently change the value of the enumeration, you must change it in the place. If you make assumptions based on the actual value of the enumerated data type, you defeat this benefit of an enumeration.

Some variations are permitted when defining an enumerated data type:The name of the data type can be omitted, and variables can be declared to be of the particular enumerated data type when the type is defined. As an example showing these of options, the statement

```
enum { east, west, south, north };
```

defines an (unnamed) enumerated data type with values east, west, south, north and declares a variable (direction) to be of that type.

Defining an enumerated data type within a block limits the scope of that definition to the block. On the other hand, defining an enumerated data type at the beginning of the program, outside any block, makes the definition global to the file.

When defining an enumerated data type, you must make certain that the enumeration identifiers are unique with respect to other variable names and enumeration identifiers defined within the same scope.

# The typedef Statement

Objective-C provides a capability that enables the programmer to assign an alternative name to a data type.This is known as typedef. The following statement defines the name Counter to be equivalent to the Objective-C data type int:
typed int Counter;