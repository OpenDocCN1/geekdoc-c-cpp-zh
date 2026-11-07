
Arrays can be declared to contain values of any nonreference data type. For example, an array of type string can be used to store character strings.

## 7.4 Examples Using Arrays

This section presents many examples that demonstrate how to declare, initialize and manipulate arrays.

### 7.4.1 Declaring an Array and Using a Loop to Initialize the Array’s Elements

The program in Fig. 7.3 declares 10-element integer array n (line 9). Lines 12–13 use a `for` statement to initialize the array elements to zeros. Like other automatic variables, automatic arrays are not implicitly initialized to zero although static arrays are. The first output statement (line 15) displays the column headings for the columns printed in the subsequent for statement (lines 18–19), which prints the array in tabular format. Remember that `setw` specifies the field width in which only the next value is to be output.

```cpp
// Fig. 7.3: fig07_03.cpp
// Initializing an array’s elements to zeros and printing the array.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
   int n[10]; // n is an array of 10 integers

   // initialize elements of array n to 0
   for (int i = 0; i < 10; ++i)
      n[i] = 0; // set element at location i to 0

   cout << "Element" << setw(13) << "Value" << endl;

   // output each array element’s value
   for (int j = 0; j < 10; ++j)
      cout << setw(7) << j << setw(13) << n[j] << endl;
} // end main
```

| Element | Value |
|---:|---:|
| 0 | 0 |
| 1 | 0 |
| 2 | 0 |
| 3 | 0 |
| 4 | 0 |
| 5 | 0 |
| 6 | 0 |
| 7 | 0 |
| 8 | 0 |
| 9 | 0 |

**Fig. 7.3** | Initializing an array’s elements to zeros and printing the array.

If the array size and an initializer list are specified in an array declaration, the number of initializers must be less than or equal to the array size. The array declaration

`int n[5] = { 32, 27, 64, 18, 95, 14 };`

causes a compilation error, because there are six initializers and only five array elements.

### 7.4.3 Specifying an Array’s Size with a Constant Variable and Setting Array Elements with Calculations

Figure 7.5 sets the elements of a 10-element array s to the even integers 2, 4, 6, ..., 20 (lines 14–15) and prints the array in tabular format (lines 17–21). These numbers are generated (line 15) by multiplying each successive value of the loop counter by 2 and adding 2.

```cpp
// Fig. 7.5: fig07_05.cpp
// Set array s to the even integers from 2 to 20.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
   // constant variable can be used to specify array size
   const int arraySize = 10;

   int s[ arraySize ]; // array s has 10 elements

   for ( int i = 0; i < arraySize; ++i ) // set the values
      s[ i ] = 2 + 2 * i;

   cout << "Element" << setw( 13 ) << "Value" << endl;

   // output contents of array s in tabular format
   for ( int j = 0; j < arraySize; ++j )
      cout << setw( 7 ) << j << setw( 13 ) << s[ j ] << endl;
} // end main
```

| Element | Value |
|---:|---:|
| 0 | 2 |
| 1 | 4 |
| 2 | 6 |
| 3 | 8 |
| 4 | 10 |
| 5 | 12 |
| 6 | 14 |
| 7 | 16 |
| 8 | 18 |
| 9 | 20 |

**Fig. 7.5** | Generating values to be placed into elements of an array.

Line 10 uses the **const qualifier** to declare a so-called **constant variable** `arraySize` with the value 10. Constant variables must be initialized with a constant expression when they’re declared and *cannot* be modified thereafter (as shown in Fig. 7.6 and Fig. 7.7). Constant variables are also called *named constants* or *read-only variables*.

> **Common Programming Error 7.2**
>
> *Not initializing a constant variable when it’s declared is a compilation error.*

![](img/bfd978e7e9b192bab46ec2a89e481263_307_0.png)

> **Common Programming Error 7.3**
>
> *Assigning a value to a constant variable in an executable statement is a compilation error.*

![](img/bfd978e7e9b192bab46ec2a89e481263_307_1.png)

```cpp
// Fig. 7.6: fig07_06.cpp
// Using a properly initialized constant variable.
#include <iostream>
using namespace std;

int main()
{
    const int x = 7;  // initialized constant variable

    cout << "The value of constant variable x is: " << x << endl;
} // end main
```

```text
The value of constant variable x is: 7
```

**Fig. 7.6** | Using a properly initialized constant variable.

```cpp
// Fig. 7.7: fig07_07.cpp
// A const variable must be initialized.

int main()
{
    const int x;  // Error: x must be initialized

    x = 7;  // Error: cannot modify a const variable
} // end main
```

*Microsoft Visual C++ compiler error message:*

```text
C:\cpphtp8_examples\ch07\fig07_07.cpp(6) : error C2734: 'x' : const object
    must be initialized if not extern
C:\cpphtp8_examples\ch07\fig07_07.cpp(8) : error C3892: 'x' : you cannot
    assign to a variable that is const
```

*GNU C++ compiler error message:*

```text
fig07_07.cpp:6: error: uninitialized const ‘x’
fig07_07.cpp:7: error: assignment of read-only variable ‘x’
```

**Fig. 7.7** | A const variable must be initialized.

In Fig. 7.7, the compilation error produced by Microsoft Visual C++ refers to the int variable x as a “const object.” The ISO/IEC C++ standard defines an “object” as any “region of storage.” Like objects of classes, fundamental-type variables also occupy space in memory, so they’re often referred to as “objects.”

Constant variables can be placed anywhere a constant expression is expected. In Fig. 7.5, constant variable `arraySize` specifies the size of array `s` in line 12.

> **Common Programming Error 7.4**
>
> *Only constants can be used to declare the size of automatic and static arrays. Not using a constant for this purpose is a compilation error.*

![](img/bfd978e7e9b192bab46ec2a89e481263_308_0.png)

Using constant variables to specify array sizes makes programs more scalable. In Fig. 7.5, the first for statement could fill a 1000-element array by simply changing the value of `arraySize` in its declaration from 10 to 1000. If the constant variable `arraySize` had not been used, we would have to change lines 12, 14 and 20 of the program to scale the program to handle 1000 array elements. As programs get larger, this technique becomes more useful for writing clearer, easier-to-modify programs.

> **Software Engineering Observation 7.1**
>
> *Defining the size of each array as a constant variable instead of a literal constant can make programs more scalable.*

![](img/bfd978e7e9b192bab46ec2a89e481263_308_1.png)

> **Good Programming Practice 7.1**
>
> *Defining the size of an array as a constant variable instead of a literal constant makes programs clearer. This technique eliminates so-called magic numbers. For example, repeatedly mentioning the size 10 in array-processing code for a 10-element array gives the number 10 an artificial significance and can be confusing when the program includes other 10s that have nothing to do with the array size.*

![](img/bfd978e7e9b192bab46ec2a89e481263_308_2.png)

### 7.4.4 Summing the Elements of an Array

Often, the elements of an array represent a series of values to be used in a calculation. For example, if the elements of an array represent exam grades, a professor may wish to total the elements of the array and use that sum to calculate the class average for the exam.

The program in Fig. 7.8 sums the values contained in the 10-element integer array `a`. The program declares, creates and initializes the array in line 9. The for statement (lines 13–14) performs the calculations. The values being supplied as initializers for array `a` also could be read into the program from the user at the keyboard, or from a file on disk (see Chapter 17, File Processing). For example, the for statement

```cpp
for ( int j = 0; j < arraySize; ++j )
    cin >> a[ j ];
```

reads one value at a time from the keyboard and stores the value in element `a[j]`.

```cpp
1  // Fig. 7.8: fig07_08.cpp
2  // Compute the sum of the elements of the array.
3  #include <iostream>
```

**Fig. 7.8** | Computing the sum of the elements of an array. (Part 1 of 2.)
