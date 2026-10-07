The only values (in theory, that is) that can be assigned to these variables are the names true and false.Thus, statements such as

```
endOfData true;
```

and

```
if ( matchFound false )
```

...

are valid.
If you want to have a specific integer value associated with an enumeration identifier, the integer can be assigned to the identifier when the data type is defined. Enumeration identifiers that subsequently appear in the list are assigned sequential integer values begin- with the specified integer value plus one.

In the following definition, an enumerated data type, direction, is defined with the values up, down, left, right:

```
enum direction { up, down, left 10, right };
```

The compiler assigns the value 0 to up because it appears first in the list, assigns 1 to down because it appears next, assigns 10 to left because it is explicitly assigned this value, and 11 to right because it is the incremented value of the preceding enum in the list.

Enumeration identifiers share the same value. For example, in

```
enum boolean { no 0, false 0, yes 1, true 1 };
```

assigning either the value no or false to an boolean variable assigns the value 0; assigning either yes or true assigns the value 1

Another example of an enumerated data type definition, the following defines the type month, with permissible values that can be assigned to a variable of this type being the number of months of the year:

```
enum month { january 1, february, march, april, may, june, july, august, september, october, december };
```

The Objective-C compiler treats enumeration identifiers as integer constants. If your program contains these two lines, the value 2 would be assigned to thisMonth (and not the name february):

...

```
thisMonth february;
```

Program 10.3 shows a simple program using enumerated data types. The program reads a month number and then enters a switch statement to see which month was entered. Recall that the compiler treats enumeration values as integer constants, so they're valid case values. The variable days is assigned the number of days in the specified month, and