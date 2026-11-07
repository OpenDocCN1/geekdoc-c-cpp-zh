
| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

We can clearly see that the rows can be controlled by one for loop (the inner loop) and the columns by another for loop (the outer loop). Now let's look at the program:

```cpp
// ForLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    int product;
    for(int leftOp = 1; leftOp <= 5; ++leftOp)
    {
        for(int rightOp = 1; rightOp <= 5; ++rightOp)
        {
            product = leftOp * rightOp;
            cout << leftOp << " x " << rightOp << " = "
                 << product << "\t";
        }
        cout << endl;
    }
    Console::ReadKey();
    return 0;
}
```

Here is the output from the program:

| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

The spacing in each row is controlled by the tab character (`\t`).

In all our previous for loops we used a single-letter variables for the loop control variable. This is acceptable since it is easy for someone reading the code to understand how the variable is being used. For this program, however, we decided to use more meaningful names for the loop control variables, leftOp and rightOp, since it helps the reader more easily understand the program.

## Exercises

- 1. Write a program that asks for the user to enter a number and then calculates the sum of the squares from 1 to that number. For example, if the user enters 4, the sum of the squares is 30 (1 + 4 + 9 + 16). The output should include the number entered by the user and the result.
- 2. Write a program that reads a set of numbers from a file and displays the number of even numbers and the number of odd numbers in the file. Hint: use the % operator to determine if a number is even or odd.
- 3. Write a program that computes the even numbers in the range from 16 to 36. Use a for loop in your program.
- 4. Using a while loop and a for loop, write a program that reads a set of numbers from a file and prints a string of asterisks for each number. The output should look like this:

  ```
  5 -   *****
  10 -  **********
  7 -   *******
  ```

## Chapter 8: Vectors

The data types we have discussed so far are useful for storing single items. A variable for storing a name can store only one name; a variable for storing a number can store only one number. Often we need the ability to store multiple values using the same variable name. One solution for this problem is the vector. A vector allows us to store multiple items of the same data type under one name. This data structure can be viewed as a list, such as a list of grades or a list of names.

### What is a Vector?

As we mentioned above, a vector can be viewed as a list of data items of the same data type. Each item in the list is specified by an index position in the list. The first item added to a vector is placed in index position 0, the next item is placed at index position 1, the next item is placed at index position 2, and so on.

Graphically, a vector looks like this (the first column is the index and the vector was declared to initially have 10 elements):

| Index | Element |
|---:|---|
| 0 | Data item |
| 1 | Data item |
| 2 | Data item |
| 3 | Data item |
| 4 | Data item |
| 5 | Data item |
| 6 | Data item |
| 7 | Data item |
| 8 | Data item |
| 9 | Data item |

One special quality of the vector is that a vector will automatically grow to accommodate new items added to the vector. This ability differentiates the vector from the array, which is similar to a vector but doesn't have the ability to grow automatically.

### Creating Vectors

Vectors are declared in a special way. Here is the general form for a vector declaration:

```cpp
vector<data type> vector-name(number of items, default-value);
```

Before you can use vectors in your C++ programs, you have to provide a preprocessor directive importing the vector class into your program. Add this line to your other preprocessor directives:

```cpp
#include <vector>
```

A vector declaration begins with the keyword vector. Next comes the data type of the elements being stored in the vector. The data type is enclosed in the less-than sign and the greater-than sign, often called angle brackets for this use. You can optionally provide the number of items you initially want to store in the vector as an argument within parentheses. You can also optionally provide a default value for the vector elements. Here are some examples of vector declarations:

```cpp
// create string vector with 20 elements
vector<string> names(20);
// create integer vector with 100 elements
vector<int> numbers(100);
// create double vector with 0 elements
vector<double> ratios;
// create int vector all 0s
vector<int> numbers(100, 0);
```

### Adding Elements to a Vector

The most common way to add elements to a vector is with the class method push_back(). This method places its argument in the next open position in the vector. The following example demonstrates how a new vector is created and is populated with two data items:

```cpp
vector<string> names;
names.push_back("Raymond");
names.push_back("Jennifer");
```

The vector looks like this:

| | |
|---|---|
| 0 | Raymond |
| 1 | Jennifer |

Every new data item added with push_back() is placed directly after the previously added data item.

Here's a code fragment that allows the user to enter names into the vector via an interactive loop:

```cpp
char answer;
string name;
cout << "Do you want to enter names? ";
cin >> answer;
while (answer == 'y')
{
    cout << "Enter a name to store in the vector: ";
    getline(cin, name);
    names.push_back(name);
    cout << "Do you want to enter more names? ";
    cin >> answer;
}
```

### Accessing Vector Elements

Vector elements are accessed by specifying their index position. For example, the following line displays the first name in the names vector above:

```cpp
cout << names[0];
```

If you want to access all the elements of a vector, use a for loop that begins at the first element of the vector and ends with the last element. One problem with using this technique is that you may not know in advance the position of the last element in the vector. You can use the vector method size(), which returns the number of elements currently in the vector.

Here is a program that stores the numbers 1 through 10 in a vector and then uses a for loop to sum the vector elements:

```cpp
// Vector.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
using namespace std;

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    for(int i = 1; i <= 10; ++i)
    {
        numbers.push_back(i);
    }
    int sum = 0;
    for(int i = 0; i < numbers.size(); ++i)
    {
        sum += numbers[i];
    }
    cout << "The sum of the integers 1 to 10 is: "
         << sum << endl;
    Console::ReadKey();
    return 0;
}
```

The output from this program is:

The sum of the integers 1 to 10 is: 55

Once you've seeded the `rand()` function you can generate a random number. You will probably want to specify a range for your random numbers. To do this, use the following formula:

```
rand() % maxNumber + 1
```

For example, if you want your random number range to be 1-100, you would use this statement to generate a random number:

```cpp
// generate random number between 1 and 100
int randomNumber = rand() % 100 + 1;
```

Adding 1 to the value ensures that the maximum value in the range may be generated by the function.

Let's look at an example of how to generate random numbers. The following program could be used as the basis for a child's guessing game where the user tries to guess a number from 1 to 10:

```cpp
// RandomNumber.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    srand(time(NULL));
    int numberToGuess = rand() % 10 + 1;
    int guess;
    cout << "Enter a guess: ";
    cin >> guess;
}
```
