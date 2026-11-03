# Enumerating constant values

The enum keyword provides a handy way to create a sequence of integer constants in a concise manner. Optionally, the declaration can include a name for the sequence after the enum keyword. The constant names follow as a comma-separated list within braces.

Each of the constants will, by default, have a value one greater than that of the constant it follows in the list. Unless specified, the first constant will have a value of zero; the next a value of 1; and so on.

For example, named weekday constants can be given a sequence of integer values starting at zero with enum(MON,TUE,WED,THU,FRI); – in this case, the constant WED has an integer value of 2.

The constants can be assigned any individual integer value in the declaration but the next constant in the list will always increment the preceding value by one, unless it too is assigned a value. For example, to begin the sequence at 1 instead of zero, assign 1 to the first constant with enum{MON=1,TUE,WED,THU,FRI}; – in this case, the constant WED has an integer value of 3.

The list of enumerated constants is also known as an "enumeration set" and may contain duplicate constant values. For example, the value zero could be assigned to constants named NIL and NONE.

In the following example, the enumeration set represents the points value of balls in the game of snooker, and includes an optional name, which appears in uppercase as it too is constant.

![](bbox=[0.2, 0.7, 0.3, 0.85])

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+      `#include <stdio.h>`
+   2. Add a main function that declares and initializes an enumerated set of constants starting at 1
+      ```c
+      int main()
+      {
+        enum SNOOKER
+        { RED=1,YELLOW, GREEN, BROWN, BLUE, PINK, BLACK };
+      }
+      ```
+   3. Next, in the main function block, declare an integer variable to store the sum of some constant values
+      `int total ;`