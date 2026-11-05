
### TABLE 2-3 C# keywords/reserved words

| Keywords |  |  |  |  |  |
|---|---|---|---|---|---|
| abstract | as | base | bool | break | byte |
| case | catch | char | checked | class | const |
| continue | decimal | default | delegate | do | double |
| else | enum | event | explicit | extern | false |
| finally | fixed | float | for | foreach | goto |
| if | implicit | in | int | interface | internal |
| is | lock | long | namespace | new | null |
| object | operator | out | override | params | private |
| protected | public | readonly | ref | return | sbyte |
| sealed | short | sizeof | stackalloc | static | string |
| struct | switch | this | throw | true | try |
| typeof | uint | ulong | unchecked | unsafe | ushort |
| using | virtual | volatile | void | while |  |

**NOTE**

Contextual keywords only have special meaning when used in a specific context. They were added in an attempt to avoid breaking code that might have been written using earlier standards where one of these words might have been used as a user-defined identifier. For example, `yield` only has a special meaning when it is used immediately before a `return` or `break` statement. Other times, it could be used as an identifier.

### TABLE 2-4 C# contextual keywords

| Contextual keywords |  |  |  |  |  |
|---|---|---|---|---|---|
| add | alias | ascending | async | await | descending |
| dynamic | equals | from | get | global | group |
| into | join | let | orderby | partial | remove |
| select | set | value | var | where | yield |

- 5. It is permissible to use the "@" symbol as the first character of an identifier, but it has special meaning and should be avoided unless you are writing code that will interface with another programming language. When used, the "@" symbol enables keywords to be used as identifiers.
- 6. It is smart to use the case of the character to your advantage. C# is case sensitive. The identifier Rate is different from the identifier rate and also different from RATE or rATE. With .NET, there are three conventions for capitalizing identifiers: Pascal case, camel case, and uppercase. Using Pascal case, the first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. Classes, methods, namespaces, and properties follow the Pascal case naming convention in C#. Variables and objects follow the camel case convention. With camel case, the first letter of an identifier is lowercase, and the first letter of each subsequent concatenated word is capitalized. The convention in C# is to use camel case for variable and object identifiers. Uppercase is used by constant literals and for identifiers that consist of two or fewer letters.
- 7. Being descriptive is helpful. Use meaningful names that represent the item being described. If the identifier is used to reference a person's age, call it age, not x. The more descriptive your identifiers, the easier it is for you and others to read your code.

Table 2-5 shows examples of valid identifiers.

### TABLE 2-5 Valid identifiers

| Valid identifiers |  |  |
|---|---|---|
| studentName | age | numberOfCourses |
| soc_sec_number | departureTime | course1 |
| AmountOwed | count_of_Values | taxAmount |
| n | streetAddress | zipCode |
| roomSize | courseName | x3 |
| moreData | bookTitle | homeRuns |
| pointsScored | CLUB_NAME | exam4 |

The compiler will not catch a violation in rule #7 of the previous list. However, this rule is extremely important, and you should follow it. By using meaningful names that describe their contents, programs you develop are more readable and easier to debug and modify. Table 2-6 shows a list of illegal identifiers and a notation indicating why they are invalid.

### TABLE 2-6 Invalid identifiers

| Invalid identifiers | Description of violation |
|---|---|
| soc sec number | Embedded space |
| int | Reserved keyword |
| 3n | Begins with a digit |
| room # | Special symbol other than underscore and an embedded space |
| first-name | Special symbol other than underscore |
| A number | Embedded space |
| class | Reserved keyword |

The rules for identifiers in C# correspond exactly to those recommended by the Unicode 3.0 standard. The only exception is that Unicode does not recognize that an underscore is allowed as an initial character. This feature was probably included in the C# language because other programming languages such as C++ allow it.

## Variables

For a computer program to process or manipulate data, the characters and numbers must be stored in random access memory (RAM). Variables are the programming elements that facilitate this storage. **A variable** represents an area in the computer memory where a value of a particular data type can be stored. When you **declare a variable**, you allocate memory for that data item in your program.

Declaring a variable requires that you select an identifier and determine what type of data will appear in the memory cell. The syntax for declaring a variable follows:

```
type identifier;
```

At the same time the variable is declared or created, it can be initialized to a value. This is referred to as a **compile-time initialization**. Notice the word initialization. The variable starts off with the initialized value, but it can be changed. The value being assigned to the variable should be compatible with the data type. When the variable is going to be used in arithmetic, it is a good idea to initialize it to 0. The syntax for initializing a variable when it is declared follows:

```
type identifier = expression;
```

The expression can simply be a value such as 0, or it can include other identifiers in an arithmetic equation.

With both types of declaration, in addition to naming the data item, you must also determine what type of data will be associated with it. This step notifies the computer of how much storage space to set aside for the data item as well as how to retrieve the data after it is placed in memory.

## Literal Values

A variable’s value can change. Literals cannot be changed. **Literals** are the numbers, characters, and combinations of characters used in your program. They can be assigned to a variable or used in an expression. Their values stay constant. The number 17 is always 17. The character A is always A. It is possible to copy the value of a literal into a variable and then change the variable; this does not change the value of the original literal. It is also possible to use literals without assigning them to a specific variable.

Every time you declare a variable in the C# language, you are actually **instantiating a class** (creating an object). If you declare three variables of `int` type, you are instantiating the class three times; three `int` objects are created. The following statement creates three `int` objects:

```
int homeWorkScore1;
int examNumber1;
int numberOfPointsScored;
```

**NOTE**

Notice how the camel case naming convention was used to declare the variables of `homeWorkScore1`, `examNumber1`, and `numberOfPointsScored`. The first letter is lowercase. The first character of subsequent words is uppercase. You were instantiating the `int` class when these objects were created. A summary of some of the C# coding standards can be found at the end of this chapter.

Literals are often used to give a value to an object’s data portion. This can be done when the object is created or later in the program statements. A value such as 100 could be assigned to `homeWorkScore1` using the following statement:

```
homeWorkScore1 = 100;
```

Here 100 is a numeric literal. The contents of the memory location where the variable `homeWorkScore1` stored the value 100 can be changed; however, the literal value of 100 cannot be changed. 100 is always 100.

**NOTE**

C# differs from languages that include a default value for variables when they are declared. In C#, every variable must be assigned a value before it is used. Otherwise, a syntax error is issued.

The next sections explain how the concept of types, classes, and objects are related to data.

## Types, Classes, and Objects

C# is an object-oriented language that makes extensive use of classes and objects. The following section explains where types fit into this picture.

### Types

C# has a large number of predefined types for use in your programs. When you think about what a type is in the English language, you probably associate type with a label that signifies the sharing of some common characteristics by a group that belongs to that
