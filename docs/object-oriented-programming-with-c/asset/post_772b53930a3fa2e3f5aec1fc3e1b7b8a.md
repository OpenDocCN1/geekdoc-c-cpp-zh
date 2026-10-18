
## Program 10.5

The output of Program 10.5 would be:

Precision set to 3 digits

| VALUE | SQRT_OF_VALUE |
|---:|---:|
| 1 | 1 |
| 2 | 1.41 |
| 3 | 1.73 |
| 4 | 2 |
| 5 | 2.24 |

Precision set to 5 digits
sqrt(10) = 3.1623
sqrt(10) = 3.162278  (default setting)

> 🡪 **NOTE:** *Observe the following from the output:*
> 
> 1. *The output is rounded to the nearest cent (i.e., 1.6666 will be 1.67 for two digit precision but 1.3333 will be 1.33).*  
> 2. *Trailing zeros are truncated.*  
> 3. *Precision setting stays in effect until it is reset.*  
> 4. *Default precision is 6 digits.*

Program 10.6 shows another program demonstrating the functionality of width and precision manipulators:

## Program 10.6  Width and Precision Manipulators

```
#include <iostream>

void main()
{
    float pi=22.0/7.0;
    int i;
    cout<<“Value of PI:\n”;
    for(i=1;i<=10;i++)
    {
        cout.width(i+1);
        cout.precision(i);
        cout<<pi<<“\n”;
    }
}
```

The output of Program 10.6 would be:

```
Value of PI:
3.1
3.14
3.143
3.1429
3.14286
3.142857
3.1428571
3.14285707
3.142857075
3.1428570747
```

## Filling and Padding: fill()

We have been printing the values using much larger field widths than required by the values. The unused positions of the field are filled with white spaces, by default. However, we can use the fill() function to fill the unused positions by any desired character. It is used in the following form:



Where chrepresents the character which is used for filling the unused positions. Example:

cout.fill('*');
cout.width(10);
cout << 5250 << "\n";

The output would be:

![](img/62b7c32e48e4f960a8dc2825a7119fb2_445_0.png)

Financial institutions and banks use this kind of padding while printing cheques so that no one can change the amount easily. Like precision(), fill() stays in effect till we change it. See Program 10.7 and its output.

## Program 10.7 Padding with Fill()

```
#include <iostream>

using namespace std;

int main( )
{ cout.fill('<');
cout.precision(3);
for(int n=1; n<=6; n++)

```

<c<<<1<<<<<<<<<<<1

<c<<<2<<<<<<<0.5

<c<<<3<<<<<0.3333

>><>4>>>>>>>>0.25

>><>5>>>>>>>>0.2

>><>6>>>>>>0.167

Padding changed

##########12.346

We have seen that when the function width() is used, the value (whether text or number) is printed right-justified in the field width created. But, it is a usual practice to print the text left-justified. How do we get a value printed left-justified? Or, how do we get a floating-point number printed in the scientific notation?

The **setf()**, a member function of the **ios** class, can provide answers to these and many other formatting questions. The **setf()** (*setf* stands for set flags) function can be used as follows:

```
cout.setf(arg1,arg2)
```

The *arg1* is one of the formatting *flags* defined in the class **ios**. The formatting flag specifies the format action required for the output. Another **ios** constant, *arg2*, known as bit *field* specifies the group to which the formatting flag belongs.

Table 10.4 shows the bit fields, flags and their format actions. There are three bit fields and each has a group of format flags which are mutually exclusive. Examples:

```
cout.setf(ios::left, ios::adjustfield);
cout.setf(ios::scientific, ios::floatfield);
```

| Format required | Flag (arg1) | Bit-field (arg2) |
|---|---|---|
| Left-justified output | ios :: left | ios :: adjustfield |
| Right-justified output | ios :: right | ios :: adjustfield |
| Padding after sign or base indicator (like +##20) | ios :: internal | ios:: adjustfield |
| Scientific notation | ios :: scientific | ios :: floatfield |
| Fixed point notation | ios :: fixed | ios :: floatfield |
| Decimal base | ios :: dec | ios :: basefield |
| Octal base | ios :: oct | ios :: basefield |
| Hexadecimal base | ios :: hex | ios :: basefield |

Note that the first argument should be one of the group members of the second argument.

Consider the following segment of code:

```
cout.fill('*');
cout.setf(ios::left, ios::adjustfield);
```

## 10.6 Managing Output with Manipulators

The header file *iomanip* provides a set of functions called *manipulators* which can be used to manipulate the output formats. They provide the same features as that of the **ios** member functions and flags. Some manipulators are more convenient to use than their counterparts in the class **ios**. For example, two or more manipulators can be used as a chain in one statement as shown below:

```
cout << manip1 << manip2 << manip3 << item;
cout << manip1 << item1 << manip2 << item2;
```

This kind of concatenation is useful when we want to display several columns of output.

The most commonly used manipulators are shown in Table 10.6. The table also gives their meaning and equivalents. To access these manipulators, we must include the file *iomanip* in the program.

**Table 10.6 — Manipulators and their meanings**

| Manipulator | Meaning | Equivalent |
|---|---|---|
| `setw (int w)` | Set the field width to w. | `width()` |
| `setprecision(int d)` | Set the floating point precision to d. | `precision()` |
| `setfill(int c)` | Set the fill character to c. | `fill()` |
| `setiosflags(long f)` | Set the format flag f. | `setf()` |
| `resetiosflags(long f)` | Clear the flag specified by f. | `unsetf()` |
| `endl` | Insert new line and flush stream. | `"\n"` |

Some examples of manipulators are given below:

```
cout << setw(10) << '12345';
```

This statement prints the value 12345 right-justified in a field width of 10 characters. The output can be made left-justified by modifying the statement as follows:

```
cout << setw(10) << setiosflags(ios::left) << i2345;
```
