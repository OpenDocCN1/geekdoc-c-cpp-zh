
| Group | Name | Operator | Expression | Prec. | Assoc. |
|---|---|---|---|---|---|
| postfix | subscript | `[]` | `name[expr]` | 18 | → |

In this case, the rest of the elements are filled with default values regardless if the array is declared in the global area or inside a function.

```cpp
const int CAPACITY = 10;
int scores[CAPACITY] = {87, 92, 100};
```

The first three elements are set to 87, 92, and 100, respectively; the rest of the elements are set to 0.

The following shows how we can explicitly initialize all elements of an array of 100 elements to 0.0.

```cpp
const int CAPACITY = 100;
double anArray[CAPACITY] = {0.0};
```

The first element is set to 0.0; the rest of the elements are set to the default value, which is also 0.0 for a floating-point type.

### 8.1.3 Accessing Array Elements

We have learned that if we want to access the contents of a variable, we must use an expression. In the case of a single variable, the name of the variable is a primary expression and we can use it to get the value stored in the variable. In the case of an array, we must use a postfix expression called subscript. The subscript expression uses the subscript operator (`[]`), with one operand. The operand is the name of the array. In Chapter 9 we show that the name of an array is actually the name of a pointer pointing to the first element. Table 8.1 provides an example of C++ expressions as shown in Appendix C.

Figure 8.4 shows how we can access an element of the array using the subscript expression.

The following shows how we can access one of the elements of each of three arrays we declared previously in Figure 8.3.

```cpp
scores[4]                         // Accessing element at location 4
nums[5]                           // Accessing element at location 5
crls[3]                           // Accessing element at location 3
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_360_0.png)

### **Program 8.1** Printing a list in reverse order (Continued)

```cpp
#include <iostream>
using namespace std;

int main ()
{
    // Declarations
    const int CAPACITY = 10;
    int numbers [CAPACITY];
    int size;
    // Getting the size from user and validate it
    do
    {
        cout << "Enter the size (1 to 10): ";
        cin >> size;
    } while (size < 1 || size > CAPACITY);
    // Inputting Integers
    cout << "Enter " << size << " integer(s): ";
    for (int i = 0; i < size; i++)
    {
        cin >> numbers[i];
    }
    // Outputting Integers in reverse order of inputting
    cout << "Integer(s) in reversed order: ";
    for (int i = size - 1; i >= 0; i--)
    {
        cout << numbers[i] << " ";
    }
    return 0;
}

Run:
Enter the size (1 to 10): 10
Enter 10 integer(s): 2 3 4 5 6 7 8 9 10 11
Integer(s) in reversed order: 11 10 9 8 7 6 5 4 3 2

Run:
Enter the size (1 to 10): 0
Enter the size (1 to 10): 11
Enter the size (1 to 10): 9
Enter 9 integer(s): 4 1 1 7 8 2 5 3 8 9    // The last integer is ignored.
Integer(s) in reversed order: 8 3 5 2 8 7 1 1 4
```

There are two important points about Program 8.1.

- 1. We do not have the out-of-range problem in this array because we forced the value of the *size* variable to be between 1 and CAPACITY in the validation loop. For example, when we have set the CAPACITY to 10, we can have between 1 and 10 integers, which fills elements with index 0 to 9; no integer goes out of the array boundaries (see the second run).

- 2. The keyboard is treated as a file in which the numbers are keyed one after another with at least one space between them. As long as the read loop is not terminated, the numbers are read one by one. Even if the user enters a return key before inputting the number of integers defined by the *size* variable, the program waits for the user to enter the rest of the integers (the return key is taken as a space). On the other hand, if the user enters more numbers than defined by the *size* variable, only the predefined number of integers is read and the rest are ignored (as in the second run, in which the last entered number, integer 9, is ignored).

### EXAMPLE 8.4

Instead of reading array elements from the keyboard, we can use an input file. A keyboard and an input file behave similarly (each acts as a source of sequential items). Also, instead of writing the array elements on the monitor after processing, we can store them in an output file. A monitor and an output file behave similarly (each acts as a destination for a sequence of data items). Program 8.2 shows how we can repeat Program 8.1, reading the original numbers from a file and writing the processed numbers to another file.

### **Program 8.2** Reversing the order of a list of numbers using files

```cpp
1 /**************************************************************
2  * Use of an array to read a list of integers from a file, to
3  * reverse the order of elements, and to write the reversed
4  * elements to another file
5  **************************************************************/
6 #include <iostream>
7 #include <fstream>
8 using namespace std;
9
10 int main ( )
11 {
12   // Declarations
13   const int CAPACITY = 50;
14   int numbers [CAPACITY];
15   int size = 0;
16   ifstream inputFile;
17   ofstream outputFile;
18   // Opening the input file
19   inputFile.open ("inFile.dat");
20   if (!inputFile)
21   {
22     cout << "Error. Input file cannot be opened." << endl;
23     cout << "The program is terminated.";
24     return 0;
25   }
26   // Reading the list of numbers from the input file into array
27   while (inputFile >> numbers[size] && size < 50)
28   {
29       size++;
30   }
31   // Closing the input file
32   inputFile.close();
33   // Opening the output file
34   outputFile.open("outFile.dat");
35   if (!outputFile)
36   {
37       cout << "Error. Output file cannot be opened." << endl;
38       cout << "The program is terminated.";
39       return 0;
40   }
41   // Writing the elements of the reversed array into the output file
42   for (int i = size - 1; i >= 0; i--)
43   {
44       outputFile << numbers[i] << " ";
45   }
46   // Closing the output file
47   outputFile.close();
48   return 0;
49 }
```

When we open the input file and the output file in a text editor, we get the following contents, in which the lists are inverse of each other.

| Input file | Output file |
|---|---|
| 12 56 72 89 11 71 61 92 34 13 | 13 34 92 61 71 11 89 72 56 12 |

There are several important points about Program 8.2:

- 1. We have included the `<fstream>` header file so we can use operations on files.
- 2. Since we do not know the count of the numbers in the input file, we must be cautious and select a large number (50 in this case) for the capacity.
- 3. If the input file is not successfully opened, we terminate the program with a message (lines 19 to 25). Similarly, if the output file is not opened successfully, we terminate the program with a message (lines 34 to 40).
- 4. The size of the array is automatically set when we reach the end of the input file (line 29).
- 5. When we run the program, we see nothing unless there is a problem with opening the input or output file.
- 6. The program never reads more than 50 integers (see line 27).

### **Program 8.3** Finding the number of days in a month of a year (Continued)

```
Run:
Enter the month number (1 to 12): 0
Enter the month number (1 to 12): 13
Enter the month number (1 to 12): 3
There are 31 days in this month.
```

Note that the first two runs reject the months less than 1 and greater than 12.

### **EXAMPLE 8.6**

In Chapter 7 we created a *Circle* class. Using the *Circle* implementation file, we can create an application program that uses the compiled version of the *Circle* class to create an array of three circles (Program 8.4).

The following shows how we can compile and link the implementation and application files to see the radius, area, and perimeter of each circle.

### **Program 8.4** Creating an array of three circles

```cpp
/* ***************************************************************
 * A program that uses the compiled version of the Circle class   *
 * to create an array of three circles.                           *
 *****************************************************************/
#include <iostream>
#include "circle.h"
using namespace std;

int main( )
{
    // Declaration of array
    Circle circles[3];
    // Instantiation of objects
    circles[0] = Circle (3.0);
    circles[1] = Circle (4.0);
    circles[2] = Circle (5.0);
    // Printing information
    for (int i = 0; i < 3; i++)
    {
        cout << "Information about circle [" << i << "]" << endl;
        cout << "Radius: " << circles[i].getRadius( ) << " ";
        cout << "Area: " << circles[i].getArea( ) << " ";
        cout << "Perimeter: " << circles[i].getPerimeter( ) << " ";
        cout << endl;
    }
    return 0;
}
```
