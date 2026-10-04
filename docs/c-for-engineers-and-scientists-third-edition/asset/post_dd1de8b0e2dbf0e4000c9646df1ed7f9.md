
# Arrays

index or subscript value. (The two terms are synonymous.) For a one-dimensional array, the first element has an index of 0, the second element has an index of 1, and so on. In C++, the array name and element index are combined by listing the index in brackets after the array name. For example, the declaration `double temp[5];` creates five elements, with the following correspondences:

- temp[0] refers to the first temperature stored in the temp array
- temp[1] refers to the second temperature stored in the temp array
- temp[2] refers to the third temperature stored in the temp array
- temp[3] refers to the fourth temperature stored in the temp array
- temp[4] refers to the fifth temperature stored in the temp array

Figure 7.2 illustrates the temp array in memory with the correct designation for each element. Each element is referred to as an indexed variable or a subscript variable because both a variable name (the array name, in this case) and an index or a subscript value must be used to reference the element. Remember that the index or subscript value gives the element's position in the array.

| temp[0] | temp[1] | temp[2] | temp[3] | temp[4] |
|---|---|---|---|---|
| temp array | element0 | element1 | element2 | element3 | element4 |

Figure 7.2 identifying array elements

The subscribed variable, temp[0], is read as "temp zero" or "temp zero." This is a shortened way of saying "the temp subscribed by zero." Similarly, temp[1] is read as "temp one" or "temp one," temp[2] as "temp two" and "temp two," and so on. Although referencing the first element with an index of 0 might seem unusual, doing so increases the computer's speed when it accesses array elements. Internally, as programmed, the computer uses the index as an offset from the array's starting position. As illustrated in Figure 7.3, the index tells the computer how many elements to skip, starting from the beginning of the array, to get to the desired element. Subscript variables can be used wherever scalar (atomic) variables are valid. Here are examples of using the elements of the temp array:

```cpp
temp[0] = 95.7;
temp[1] = -10.0;
temp[2] = 5.0 * temp[0];
temp[3] = 72.0;
temp[4] = (temp[1] + temp[2]) / 2.2;
sum = temp[0] + temp[1] + temp[2] + temp[3] + temp[4];
```

The subscript in brackets needs not be an integer constant; any expression that evaluates to an integer can be used as a subscript. In each case, the value of the expression identifies the starting location of the array:

```cpp
temp[0]
temp[1]
temp[2]
temp[3]
temp[4]
```

**Figure 7.3** Accessing an array—the index must be within the valid range defined when the array is declared. For example, assuming i and j are variables, the following subscribed variables are valid:

```cpp
temp[i]
temp[j]
```

An advantage of using integer expressions as subscripts is that it allows sequencing through an array by using a loop. This makes statements as the following unnecessary:

```cpp
sum = temp[0] + temp[1] + temp[2] + temp[3] + temp[4];
```

The subscript values can be replaced by a loop counter to access each element in the array. For example, the code:

```cpp
sum = 0; // initialize the sum to zero
for (i = 0; i < 5; i++) // add a value
    sum = sum + temp[i];
```

retrieves each element in the loop and adds it to the sum. The variable i is used as both the counter and the index referenced. As i increases by one, the next element in the array is referenced. The procedure for adding array elements in the loop is similar to the accumulation procedure you have used before.

The advantage of using a loop to sequence through an array becomes apparent when working with larger arrays. For example, if the array contains 100 values rather than just 5, simply changing the number of iterations to 100 is enough to sequence through the 100 elements and add each temperature to the sum.

As another example of using a loop to sequence through an array, say you want to locate the maximum value in an array of 1000 elements named voltage. The procedure to locate the maximum value is to assume initially that the first element in the array is the largest number. Then, as you sequence through the array, the maximum is compared to each element.

## Aggregate Data Types

In contrast to atomic types, such as integer and floating-point data, there are aggregate types. An **aggregate type**, also referred to as both a structured type and a data structure, is one whose values can be decomposed and are related by some defined structure. Additionally, operations must be available for retrieving and updating values in the data structure.

One-dimensional arrays are examples of a structured type. In a one-dimensional array, as an array of integers, the array is composed of integer values, with the integers referred by their position in the index. Indexed variables provide the means of accessing and modifying values in the array. When an element with a higher value is located, element becomes the maximum. The following code does the job:

```cpp
const int NUMELS = 5;
maximum = volts[0];               // set the maximum to element 0
for (int i = 1; i < NUMELS; i++) // cycle through the rest of the array
    if (volts[i] > maximum)      // compare each element to the maximum
        maximum = volts[i];          // capture the new high value
```

In this code, the first statement consists of one element. The search for new maximum value starts with element 1 of the array and continues through the last element. Each element is compared to the current maximum, and when a higher value is encountered, it becomes the new maximum.

## Input and Output of Array Values

An array can be assigned a value interactively by using a cin statement, as shown in these examples of data entries:

```cpp
cin >> temp[0];
cin >> temp[1] >> temp[2] >> temp[3];
cin >> temp[4] >> volts[6];
```

In the first statement, a single value is read and stored in the variable temp[0]. The second statement causes three values to be read and stored in the variables temp[1], temp[2], and temp[3]. Finally, the last cin statement reads into temp[4] and volts[6].

Alternatively, a loop can be used for interactive input. For example, the code below prompts for five variables:

```cpp
const int NUMELS = 5;
for(int i = 0; i < NUMELS; i++) {
    cout << "Enter temperature: ";
    cin >> temp[i];
}
```

## One-Dimensional Arrays

One caution about storing data in an array: C++ does not check the value of the index being used (called a bounds check). If an array has been declared as consisting of 10 elements, for example, and if you use an index of 12, which is outside the bounds of the array, C++ will not notify you of the error when it is compiled. The program attempts to access index 12 by skipping the appropriate number of bytes from the start of the array. Usually, this attempt returns a value of the correct type, but simply overwrites memory locations. This leads to more errors, which are troublesome to locate when the value legitimately assigned to storage is at a different point in the program.

During output, an element can be displayed using a cout statement, or complete sections of the array can be displayed by including a cout statement in a loop. Both of these methods are shown:

```cpp
cout << volts[6];
```

```cpp
cout << "The value of element " << i << " is " << temp[i];
```

```cpp
int NUMELS = 20;
for (int k = 5; k < NUMELS; k++)
    cout << k << " " << amount[k] << endl;
```

Program 7.1 illustrates these input and output techniques, using an array named temp defined to store five integer numbers. The program includes for two loops. The first loop is used to cycle through each array element and allows the user to input array values. After five values have been entered, the second loop is used to display the stored values.

# Program 7.1

```cpp
#include <iostream>
using namespace std;

int main()
{
    const int MAXTEMPS = 5;
    int i, temp[MAXTEMPS];
```
