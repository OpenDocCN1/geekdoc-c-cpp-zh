
- d. Given the declaration:

  ```cpp
  int list[10];
  ```

  the statement:

  ```cpp
  list[5] = list[3] + list[2];
  ```

  updates the content of the fifth component of the array list. (2)

- e. If an array index goes out of bounds, the program always terminates in an error. (3)

- f. The only aggregate operations allowable on `int` arrays are the increment and decrement operations. (5)

- g. Arrays can be passed as parameters to a function either by value or by reference. (6)

- h. A function can return a value of type array. (6)

- i. In C++, some aggregate operations are allowed for strings. (11, 12, 13)

- j. The declaration:

  ```cpp
  char name[16] = "John K. Miller";
  ```

  declares name to be an array of 15 characters because the string "John K. Miller" has only 14 characters. (11)

- k. The declaration:

  ```cpp
  char str = "Sunny Day";
  ```

  declares str to be a string of an unspecified length. (11)

- l. As parameters, two-dimensional arrays are passed either by value or by reference. (15, 16)

### 2. Consider the following declaration: (1, 2)

```cpp
int accountNum[75];
```

In this declaration, identify the following:

- a. The array name.
- b. The array size.
- c. The data type of each array component.
- d. The range of values for the index of the array.
- e. The index of the first element.
- f. The index of the last element.

### 3. Identify error(s), if any, in the following array declarations. If a statement is incorrect, provide the correct statement. (1, 2)

- a. `int primeNum[99];`
- b. `int testScores[0];`
- c. `string names[60];`
- d. `int list100[0..99];`
- e. `double[50] gpa;`
- f.

  ```cpp
  const double LENGTH = 26;
  double list[LENGTH - 1];
  ```

- g.

  ```cpp
  const long SIZE = 100;
  int list[2 * SIZE];
  ```

### 4. Determine whether the following array declarations are valid. If a declaration is invalid, explain why. (1, 2)

- a. `string customers[];`
- b. `int numArray[50];`
- c.

  ```cpp
  const int SIZE = 30;
  double list[20 - SIZE];
  ```

- d.

  ```cpp
  int length = 50;
  double list[length - 50];
  ```

- e. `int ids[-30];`
- f. `colors[30] string;`

### 5. What would be a valid range for the index of an array of size 99? What is the index of the first element? What is the index of the last element? (1, 3)

### 6. Write C++ statement(s) to do the following: (1, 2)

- a. Declare an array `alpha` of 50 components of type `int`.
- b. Initialize each component of `alpha` to −1.
- c. Output the value of the first component of the array `alpha`.
- d. Set the value of the twenty-fifth component of the array `alpha` to 62.
- e. Set the value of the tenth component of `alpha` to three times the value of the fiftieth component of `alpha` plus 10.
- f. Use a `for` loop to output the value of a component of `alpha` if its index is a multiple of 2 or 3.
- g. Output the value of the last component of `alpha`.
- h. Output the value of `alpha` so that 15 components per line are printed.
- i. Use a `for` loop to increment every other element (the even indexed elements).
- j. Use a `for` loop to create a new array, `diffAlpha`, whose elements are the differences between consecutive elements in `alpha`.

### 7. What is the output of the following program segment? (2)

```cpp
int temp[5];

for (int i = 0; i < 5; i++)
    temp[i] = static_cast<int>(pow(i, 2.0));

for (int i = 0; i < 5; i++)
    cout << temp[i] << " ";
cout << endl;

temp[4] = temp[3] * temp[2];
temp[3] = temp[4] - temp[2];
temp[0] = temp[5] - temp[1];

for (int i = 0; i < 5; i++)
    cout << temp[i] << " ";
cout << endl;
```

### 8. What is stored in list after the following C++ code executes? (2)

```cpp
int list[10];

for (int i = 0; i < 5; i++)
{
    list[i] = i * (i - 1);
    if (i % 2 == 0)
        list[i] = list[i] + i;
    else if (i % 3 == 0)
        list[i] = list[i] - i;
    else if (i > 0)
        list[i] = list[i] - list[i - 1];
}
```

### 9. What is stored in list after the following C++ code executes? (2)

```cpp
int list[8];

list[0] = 1;
list[1] = 2;
for (int i = 2; i < 8; i++)
{
    list[i] = list[i - 1] * list[i - 2];
    if (i > 5)
        list[i] = list[i] - list[i - 1];
}
```

### 10. What is stored in myList after the following C++ code executes? (2)

```cpp
double myList[6];

myList[0] = 2.5;

for (int i = 1; i < 6; i++)
{
    myList[i] = i * myList[i - 1];
    if (i > 3)
        myList[i] = myList[i] / 2;
}
```

### 11. Correct the following code so that it correctly sets the value of each element of myList to the index of the element. (2, 3)

```cpp
int myList[10];

for (int i = 1; i > 10; i++)
    myList[i] = i;
```

### 12. Correct the following code so that it correctly initializes and outputs the elements of the array `myList`. (2, 3)

```cpp
int myList[10];

for (int i = 1; i <= 10; i++)
    cin >> myList;

for (int i = 1; i <= 10; i++)
    cout << myList[i] << " ";
cout << endl;
```

### 13. What is array index out of bounds? Does C++ check for array indices within bounds? (3)

### 14. Suppose that `scores` is an array of 10 components of type `double`, and:

`scores = {2.5, 3.9, 4.8, 6.2, 6.2, 7.4, 7.9, 8.5, 8.5, 9.9}`

The following is supposed to test that the elements of scores are in nondecreasing order. However, there are errors in the code. Find and correct the errors. (1, 2, 3)

```cpp
for (int i = 1; i <= 10; i++)
    if (scores[i] >= scores[i + 1])
        cout << " " << i << " and " << (i + 1)
             << " elements of scores are out of order." << endl;
```

### 15. Write C++ statements to define and initialize the following arrays. (4)

- a. Array `heights` of 10 components of type `double`. Initialize this array to the following values: 5.2, 6.3, 5.8, 4.9, 5.2, 5.7, 6.7, 7.1, 5.10, 6.0.
- b. Array `weights` of 7 components of type `int`. Initialize this array to the following values: 120, 125, 137, 140, 150, 180, 210.
- c. Array `specialSymbols` of type `char`. Initialize this array to the following values: '$', '#', '%', '@', '&', '!', '^'.
- d. Array `seasons` of 4 components of type `string`. Initialize this array to the following values: "fall", "winter", "spring", "summer".

### 16. Determine whether the following array declarations are valid. If a declaration is valid, determine the size of the array. (4)

- a. `int list[] = {18, 13, 14, 16};`
- b. `int x[10] = {1, 7, 5, 3, 2, 8};`
- c. `double y[4] = {2.0, 5.0, 8.0, 11.0, 14.0};`
- d. `double lengths[] = {8.2, 3.9, 6.4, 5.7, 7.3};`
- e. `int list[7] = {12, 13, , 14, 16, , 8};`
- f. `string names[8] = {"John", "Lisa", "Chris", "Katie"};`

### 17. Suppose that you have the following declaration:

```cpp
int list[8] = {6, 10, 14, 18, 22};
```

If this declaration is valid, what is stored in each of the eight components of list. (4)

### 18. Consider the following declaration: (2)

```cpp
int list[] = {3, 8, 10, 13, 6, 11};
```

- a. Write a C++ code that will output the value stored in each component of list.
- b. Write a C++ code that will set the values of the first five components of list as follows: The value of the ith component is the value of the ith component minus three times the value of the (i+1)th component.

### 19. What is the output of the following C++ code? (2)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int beta[7] = {3, 5};

    for (int i = 2; i < 7; i++)
    {
        beta[i] = 3 * i + 2;
        beta[i - 1] = beta[i - 1] + beta[i];
        beta[i - 2] = beta[i - 2] + beta[i - 1];
    }

    for (int i = 0; i < 7; i++)
        cout << beta[i] << " ";
    cout << endl;

    return 0;
}
```

### 20. What is the output of the following C++ code? (2)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int list1[5];
    int list2[15];

    for (int i = 0; i < 5; i++)
        list1[i] = i * i - 2;

    cout << "list1: ";
    for (int i = 0; i < 5; i++)
        cout << list1[i] << " ";
    cout << endl;
```
