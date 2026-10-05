# 1.1.3 Using Structures in Application Programs

The steps to use this new data type are as follows:
Step 1: Include the header file provided by the library programmer in the source code.

```
/*Beginning of dateUser.C*/
#include="date.h"
void main()
{
    ....
    ....
}
/*End of dateUser.C*/
```

Step 2: Declare variables of the new data type in the source code.

```
/*Beginning of dateUser.C*/
#include="date.h"
void main()
{
    struct date d;
    ....
    ....
}
/*End of dateUser.C*/
```

Step 3: As shown in Listing 1.5, embed calls to the associated functions by passing these variables in the source code.

Listing 1.5 Using a structure in an application program

```
/*Beginning of dateUser.C*/
#include="date.h"
void main()
{
    struct date d;
d.d=28;
d.m=2;
d.y=1999;
    next_day(&d);
    ....
    ....
}
/*End of dateUser.C*/
```

Step 4: Compile the source code to get the object file.
Step 5: Link the object file with the library provided by the library programmer to get the executable or another library.

# 1.2 Procedure-Oriented Programming Systems

In light of the previous discussion, let us understand the procedure-oriented programming system. The forming of programming code into functions. Data (contained in structure variables) is passed from one function to another to be read or written into. The focus is on procedures. This programming pattern is, therefore, a feature of the procedure-oriented programming system.