# Defining type structures

A data type defined by a structure can be declared to be an actual data type definition by adding the typedef keyword at the very beginning of the structure declaration. This identifies the structure to be a prototype from which other structures can be declared simply using any of its tag names – without the struct keyword.

Using typedef may often help simplify the code by not requiring the struct keyword when declaring variables of a data type defined in a structure. It is helpful, however, to capitalize the tag name so it is easily recognizable as a structure-defined data type.

Declarations of variables of data types defined in a structure may optionally initialize all their members by assigning values as a comma-separated list within braces.

Structures may also be nested within other structures. In that case, individual members are referenced using two "." dot operators, with the syntax outer-structure.inner-structure.member.

+   Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

+   Declare an un-named structure defining a data type with two members and one tag

```
typedef struct
{
int x;
int y;
} Point;
```