
## Commenting Data Declarations

Cross-Reference For details on formatting data, see "Laying Out Data Declarations" in Section 31.5. For details on how to use data effectively, see Chapters 10 through 13.

Comments for variable declarations describe aspects of the variable that the variable name can’t describe. It’s important to document data carefully; at least one company that studied its own practices has concluded that annotations on data are even more important than annotations on the processes in which the data is used (SDC, in Glass 1982). Here are some guidelines for commenting data:

**Comment the units of numeric data** If a number represents length, indicate whether the length is expressed in inches, feet, meters, or kilometers. If it’s time, indicate whether it’s expressed in elapsed seconds since 1-1-1980, milliseconds since the start of the program, and so on. If it’s coordinates, indicate whether they represent latitude, longitude, and altitude and whether they’re in radians or degrees; whether they represent an X, Y, Z coordinate system with its origin at the earth’s center; and so on. Don’t assume that the units are obvious. To a new programmer, they won’t be. To someone who’s been working on another part of the system, they won’t be. After the program has been substantially modified, they won’t be.

Alternatively, in many cases you should embed the units in the variable names rather than in comments. An expression like *distanceToSurface = marsLanderAltitude* looks like it’s probably correct, but *distanceToSurfaceInMeters = marsLanderAltitudeInFeet* exposes an obvious error.

Cross-Reference A stronger technique for documenting allowable ranges of variables is to use assertions at the beginning and end of a routine to assert that the variable’s values should be within a prescribed range. For more details, see Section 8.2, "Assertions."

**Comment the range of allowable numeric values** If a variable has an expected range of values, document the expected range. One of the powerful features of the Ada programming language was the ability to restrict the allowable values of a numeric variable to a range of values. If your language doesn’t support that capability (and most languages don’t), use a comment to document the expected range of values. For example, if a variable represents an amount of money in dollars, indicate that you expect it to be between $1 and $100. If a variable indicates a voltage, indicate that it should be between 105v and 125v.

**Comment coded meanings** If your language supports enumerated types—as C++ and Visual Basic do—use them to express coded meanings. If it doesn’t, use comments to indicate what each value represents—and use a named constant rather than a literal for each of the values. If a variable represents kinds of electrical current, comment the fact that 1 represents alternating current, 2 represents direct current, and 3 represents undefined.

Here’s an example of documenting variable declarations that illustrates the three preceding recommendations—all the range information is given in comments:

**Visual Basic Example of Nicely Documented Variable Declarations**

```vb
Dim cursorX As Integer   ' horizontal cursor position; ranges from 1..MaxCols
Dim cursorY As Integer   ' vertical cursor position; ranges from 1..MaxRows

Dim antennaLength As Long      ' length of antenna in meters; range is >= 2
Dim signalStrength As Integer  ' strength of signal in kilowatts; range is >= 1

Dim characterCode As Integer     ' ASCII character code; ranges from 0..255
Dim characterAttribute As Integer ' 0=Plain; 1=Italic; 2=Bold; 3=Bold+Italic
Dim characterSize As Integer      ' size of character in points; ranges from 4..127
```

**Comment limitations on input data** Input data might come from an input parameter, a file, or direct user input. The previous guidelines apply as much to routine-input parameters as to other kinds of data. Make sure that expected and unexpected values are documented. Comments are one way of documenting that a routine is never supposed to receive certain data. Assertions are another way to document valid ranges, and if you use them the code becomes that much more self-checking.

**Document flags to the bit level** If a variable is used as a bit field, document the meaning of each bit:

> **Cross-Reference** For details on naming flag variables, see "Naming Status Variables" in Section 11.2.

**Visual Basic Example of Documenting Flags to the Bit Level**

```vb
• The meanings of the bits in statusFlags are as follows, from most
  significant bit to least significant bit:
• MSB    0       error detected: 1=yes, 0=no
         1–2     kind of error: 0=syntax, 1=warning, 2=severe, 3=fatal
         3       reserved (should be 0)
         4       printer status: 1=ready, 0=not ready
         ...
         14      not used (should be 0)
• LSB    15–32   not used (should be 0)
Dim statusFlags As Integer
```

If the example were written in C++, it would call for bit-field syntax so that the bit-field meanings would be self-documenting.

**Stamp comments related to a variable with the variable’s name** If you have comments that refer to a specific variable, make sure the comment is updated whenever the variable is updated. One way to improve the odds of a consistent modification is to stamp the comment with the variable name. That way, string searches for the variable name will find the comment as well as the variable.

> **Cross-Reference** For details on using global data, see Section 13.3, "Global Data."

**Document global data** If global data is used, annotate each piece well at the point at which it’s declared. The annotation should indicate the purpose of the data and why it needs to be global. At each point at which the data is used, make it clear that the data is global. A naming convention is the first choice for highlighting a variable’s global status. If a naming convention isn’t used, comments can fill the gap.

loops that aren’t nested. When the nesting is deep or the loops are long, however, the technique pays off.

*Treat end-of-loop comments as a warning indicating complicated code* If a loop is complicated enough to need an end-of-loop comment, treat the comment as a warning sign: the loop might need to be simplified. The same rule applies to complicated if tests and case statements.

End-of-loop comments provide useful clues to logical structure, but writing them initially and then maintaining them can become tedious. The best way to avoid such tedious work is often to rewrite any code that’s complicated enough to require tedious documentation.

## Commenting Routines

Cross-Reference For details on formatting routines, see Section 31.7. For details on how to create high-quality routines, see Chapter 7.

![](img/649c8eee28c38ca1e062691e45dc9883_841_0.png)

Routine-level comments are the subject of some of the worst advice in typical computer-science textbooks. Many textbooks urge you to pile up a stack of information at the top of every routine, regardless of its size or complexity:

Visual Basic Example of a Monolithic, Kitchen-Sink Routine Prolog

```text
********************************************************************************
* Name: CopyString
*
* Purpose:     This routine copies a string from the source
               string (source) to the target string (target).
*
* Algorithm:   It gets the length of "source" and then copies each
               character, one at a time, into "target". It uses
               the loop index as an array index into both "source"
               and "target" and increments the loop/array index
               after each character is copied.
*
* Inputs:      input    The string to be copied
*
* Outputs:     output   The string to receive the copy of "input"
*
* Interface Assumptions: None
*
* Modification History: None
*
* Author:      Dwight K. Coder
* Date Created: 10/1/04
* Phone:       (555) 222-2255
* SSN:         111-22-3333
* Eye Color:   Green
* Maiden Name: None
* Blood Type:  AB-
* Mother's Maiden Name: None
* Favorite Car: Pontiac Aztek
* Personalized License Plate: "Tek-ie"
********************************************************************************
```
