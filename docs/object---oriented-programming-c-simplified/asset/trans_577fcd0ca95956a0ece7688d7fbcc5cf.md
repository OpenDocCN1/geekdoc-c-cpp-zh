

    cout << a << endl;
    cout.width(8);

    cout << b << endl;
    cout.width(8);

    cout << c << endl;
    cout.width(8);

    cout << d << endl;
    cout.width(8);

    cout << e << endl;
    cout << "==================================================" << endl;
    getch( );
```

**OUTPUT:**

```
==================================================
THE PATTERN IS GIVEN AS
==================================================
12345
1234
123
12
1
==================================================
```

**EXPLANATION :** The width function first set the width of 8 characters and then displays the data followed in the width of 8 starting from right justified and left padded. For each data to be printed, separated width has to be set first.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_547_0.png)

Figure 11.5. Demo of width function

## Input-Output and Manipulators in C++

```cpp
/*PROG 11.12 DEMO OF WIDTH FUNCTION VER 2*/
#include <iostream.h>
#define S 5
#include <conio.h>

void main()
{
int arr[S], i;

clrscr();
cout << " Enter the " << S << " numbers" << endl;
for(i=0;i<S;i++)
{
cin >> arr[i];
}
cout.width(10);
cout << "--------------------------------" << endl;
cout << " Number";
cout << " Square";
cout << endl;
for(i=0;i<S;i++)
{
cout.width(10);
cout << arr[i];
cout.width(10);
cout << arr[i]*arr[i];
cout << endl;
}
cout << "--------------------------------" << endl;
getch();
}
```

**OUTPUT:**

```
Enter the 5 numbers
47
78
98
99
156
```

| Number | Square |
|---:|---:|
| 47 | 2209 |
| 78 | 6084 |
| 98 | 9604 |
| 99 | 9801 |
| 156 | 24336 |

**EXPLANATION:** For displaying Number and Square as heading we set the width 10. In the for loop for displaying the number and their square same width is set again.

```cpp
/*PROG 11.13 DEMO OF WIDTH AND FILL FUNCTION TOGETHER */
#include <iostream.h>
#include <conio.h>
void main( )
{
    int a = 12345, b = 1234, c= 123, d = 12, e=1;
    clrscr( );
    cout << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl;
    cout << "DEMO OF fill AND width FUNCTION" << endl;
    cout << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl << endl;
    cout.fill('$');
    cout.width(8);
    cout << a << endl;
    cout.width(8);
    cout << b << endl;
    cout.width(8);
    cout << c << endl;
    cout.width(8);
    cout << d << endl;
    cout.width(8);
    cout << e << endl;
    cout << endl << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl;
    getch( );
}
```

**OUTPUT:**

```
+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*
DEMO OF fill AND width FUNCTION
+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*

$$$12345
$$$$1234
$$$$$123
$$$$$$12
$$$$$$$1
+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*
```

**EXPLANATION :** If whole of the width allocated is not utilized by the data to be printed, remaining empty spaces can be filled using `cout.fill()` method. The fill function takes a character as argument which acts as a filling character. Once this is set extra spaces will be filled by character specified as argument to fill method.

The output of the above program can be shown diagrammatically as follows :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_550_0.png)

Figure 11.6. Demo of fill and width function together.

```cpp
/*PROG 11.14 DEMO OF PRECISION FUNCTION */

#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();

    cout << "#########################" << endl;
    cout << " DEMO OF PRECISION FUNCTION" << endl;
    cout << "#########################" << endl;

    cout.precision(3);
    cout << "\t" << 123.12345 << endl;

    cout.precision(4);
    cout << "\t" << 345.656767 << endl;

    cout.precision(10);
    cout << "\t" << 22/7.0 << endl;

    cout << endl;
    cout << "################################" << endl;
    getch();
}
```

**OUTPUT:**

```
################################
DEMO OF PRECISION FUNCTION
################################
123.123
345.6568
3.1428571429
################################
```

**EXPLANATION :** In the program we have set the precision at 3 different places and all are different. Program can be best understood by viewing the output of the program.

```cpp
/*PROG 11.15 DEMO OF width AND precision FUNCTION TOGETHER IN A SINGLE PROGRAM */

#include <iostream.h>
#include <conio.h>
#include <math.h>

#define S 5
void main()
{
    float arr[S]={34.0, 79.0, 67.0, 33.0, 24.0};
    int i;
    clrscr();
    cout << "#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$" << endl;
    cout << "DEMO OF WIDTH AND PRECISION FUNCTION TOGETHER" << endl;
    cout << "#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$#$" << endl;
    cout.precision(4);

    cout << endl << "+++++++++++++++++++++++++++++++++++++++++++++" << endl;
    cout.width(8);
    cout << "Number";
    cout.width(15);
```

**Table 11.1 : Formatted Flags Used in C++**

| S.No. | Flags | Mask | Output |
|---:|---|---|---|
| 1. | `ios::left` | `ios::adjustfield` | Left justified |
| 2. | `ios::right` | `ios::adjustfield` | Right justified |
| 3. | `ios::internal` | `ios::adjustfield` | Add fill characters after any leading sign or base indication |
| 4. | `ios::scientific` | `ios::floatfield` | Scientific notation |
| 5. | `ios::fixed` | `ios::floatfield` | Fixed point notation |
| 6. | `ios::dec` | `ios::basefield` | Output in decimal |
| 7. | `ios::hex` | `ios::basefield` | Output in hex |
| 8. | `ios::oct` | `ios::basefield` | Output in octal |

### (g) The Second Syntax of setf is :

```
long setf (long flags);
```

Function turns on only those format bits that are specified by 1s in flags. It returns a long that contains the previous values of all the flags. These are the flags which are used independently without the use of Mask parameter. The table given below lists all the flags :

**Table 11.2 : Formatted Flags Used in C++**

| S.No. | Flags | Purpose |
|---:|---|---|
| 1. | `ios::showpoint` | Show decimal point and trailing zero for floating-point values. |
| 2. | `ios::showbase` | Display numeric constants in a format that can be read by the C++ compiler. |
| 3. | `ios::showpos` | Show plus sign (+) for positive values. |
| 4. | `ios::uppercase` | Display uppercase A through F for hexadecimal values and E for scientific values. |
| 5. | `ios::skipws` | Skip white space on input |
| 6. | `ios::unitbuf` | Flush the stream after each insertion. |
| 7. | `ios::stdio` | Flush stdout and stderr after each insertion |

```cpp
/*PROG 11.16 DEMO OF FORMATTING FLAGS VER 1*/

#include <iostream.h>
#include <conio.h>
void main()
{
    char s[] = "Hello";
    clrscr();
    cout << "___________________________" << endl;
    cout << "STRING WITHOUT SETTING WIDTH\n";
    cout << "___________________________" << endl;
    cout << s << endl;
    cout << endl << "___________________________" << endl;
    cout << "STRING AFTER SETTING WIDTH AND PADDING" << endl;
    cout << "___________________________" << endl;
    cout << "RIGHT JUSTIFIED" << endl;
    cout << "___________________________" << endl;
    cout.fill('&');
    cout.setf(ios::right, ios::adjustfield);
    cout.width(15);
    cout << s << endl;
    cout << "___________________________" << endl;
    cout << "LEFT JUSTIFIED" << endl;
    cout << "___________________________" << endl;
    cout.fill('&');
    cout.setf(ios::left, ios::adjustfield);
    cout.width(15);
    cout << s << endl;
    cout << "___________________________" << endl;
    getch();
}
```

**OUTPUT:**

```
___________________________
STRING WITHOUT SETTING WIDTH
___________________________
Hello
___________________________
STRING AFTER SETTING WIDTH AND PADDING
___________________________
RIGHT JUSTIFIED
___________________________
&&&&&&&&&&Hello
___________________________
LEFT JUSTIFIED
___________________________
Hello&&&&&&&&&&
___________________________
```

**EXPLANATION :** For the following settings :

```
cout.fill('&');
cout.setf(ios::right, ios::adjustfield);
cout.width(15);
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_555_0.png)

Figure 11.7. Implementation of ios flags

Now, by changing `ios::right` to `ios::left` we get the output as :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_555_1.png)

Figure 11.8. Implementation of ios flags

