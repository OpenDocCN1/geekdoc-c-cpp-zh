# Table 11.1 : Formatted Flags Used in C++

| S.No. | Flags | Mask | Output |
|---|---|---|---|
| 1. | ios ::left | ios ::adjustfield | Left justified |
| 2. | ios ::right | ios ::adjustfield | Right justified |
| 3. | ios ::internal | ios ::adjustfield | Add fill characters after any leading sign or base indication |
| 4. | ios ::scientific | ios ::floatfield | Scientific notation |
| 5. | ios ::fixed | ios ::floatfield | Fixed point notation |
| 6. | ios ::dec | ios ::basefield | Output in decimal |
| 7. | ios ::hex | ios ::basefield | Output in hex |
| 8. | ios ::oct | ios ::basefield | Output in octal |

# (g) The Second Syntax of setf is :

```
long setf (long flags);
```

Function turns on only those format bits that are specified b 1s in flags. It returns a long that contains the previous values of all the flags. These are the flags which are used independently without the use of Mask parameter. The table given below lists all the flags :

# Table 11.2 : Formatted Flags Used in C++

| S.No. | Flags | Purpose |
|---|---|---|
| 1. | ios ::showpoint | Show decimal point and trailing zero for floating-point values. |
| 2. | ios ::showbase | Display numeric constants in a format that can be read by the C++ compiler. |
| 3. | ios ::showpos | Show plus sign (+) for positive values. |
| 4. | ios ::uppercase | Display uppercase A through F for hexadecimal values and E for scientific values. |
| 5. | ios ::skipws | Skip white space on input |
| 6. | ios ::unitbuf | Flush the stream after each insertion. |
| 7. | ios ::stdio | Flush stdout and stderr after each insertion |

```
/*PROG 11.16 DEMO OF FORMATTING FLAGS VER 1*/

#include <iostream.h>
#include <conio.h>
void main()
{
    char s[] = "Hello";
```