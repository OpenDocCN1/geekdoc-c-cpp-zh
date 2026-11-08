
If the user guesses the number correctly, the program exits; otherwise, the program asks the user if he or she wants to guess again. If the user enters a “Y”, you let him or her guess again. If the user enters “N”, the loop exits. You can see that the user entering a “Y” or an “N” is the sentinel value that controls the loop. Note that the entire program has been written for you. You need to add code that validates correct input, which is a Y or an N when the user is asked if he or she wants to guess a number, and a number in the range of 1 through 10 when the user is asked to guess a number.

- 1. Open the source code file named `GuessNumber.cpp` using Notepad or the text editor of your choice.
- 2. Write loops that validate input at all places in the code where the user is asked to provide input. Comments have been included in the code to help you identify where these loops should be written.
- 3. Save this source code file in a directory of your choice and then make that directory your working directory.
- 4. Compile the source code file `GuessNumber.cpp`.
- 5. Execute the program. See if you can guess the randomly generated number. Execute the program several times to see if the random number changes. Also, test the program to verify that incorrect input is handled correctly. On your best attempt, how many guesses did you have to take to guess the correct number? ________

## 6 USING ARRAYS IN C++ PROGRAMS

**After studying this chapter, you will be able to:**

- Use arrays in C++ programs
- Search an array for a value
- Use parallel arrays in a C++ program

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_108_0.png)

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_108_1.png)

You should do the exercises and labs in this chapter after you have finished Chapter 6 of *Programming Logic and Design, Fifth Edition*, by Joyce Farrell. In this chapter, you learn how to use C++ to declare and initialize arrays. You then access the elements of an array to assign values and process them within your program. You also learn why it is important to stay within the bounds of an array. In addition, you study some programs written in C++ that implement the logic and design presented in *Programming Logic and Design, Fifth Edition*.

### ARRAY BASICS

An **array** is a group of data items in which all items have the same data type, are referenced using the same variable name, and are stored in consecutive memory locations. To reference an individual element in an array, you use a subscript. Think of a **subscript** as the position number of a value within an array. It is important for you to know that in C++, subscript values begin with 0 (zero) and end with *n*-1, where *n* is the number of items stored in the array.

To use an array in a C++ program, you must first learn how to declare an array, initialize an array with predetermined values, access array elements, and stay within the bounds of an array. In the next section you’ll focus on the first step, declaring arrays.

### DECLARING ARRAYS

Before you can use an array in a C++ program, you must first declare it. That is, you must give it a name and specify the data type for the data that will be stored in it. In some cases, you also specify the number of items that will be stored in the array. The following code shows how to declare an array named `cityPopulations` that will be used to store four `int`s, and an array named `cities` that will be used to store four `string`s:

```cpp
int cityPopulations[4];
string cities[4];
```

As you can see in this example, you begin by specifying the data type of the items that will be stored in the array. The data type is followed by the name of the array and then a pair of square brackets. Within the square brackets, you see an integer value that specifies the number of elements this array can hold.

As shown in Figure 6-1, the compiler allocates enough consecutive memory locations to store four elements of data type `int` for the array named `cityPopulations`. If `cityPopulations[0]` is stored at memory address 1000, then the address of `cityPopulations[1]` is 1004 because each `int` requires 4 bytes of memory. Similarly, `cityPopulations[3]` is at address 1012.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_109_0.png)

> **NOTE**
> 
> If an array is declared to store items of data type `double`, 8 bytes are allocated for each item in the array.

The `cityPopulations` array provides an example of how memory is allocated for arrays that contain primitive data types. Memory allocation is different for arrays of `strings` because a `string` is an object in C++, not a primitive data type. Using the Visual C++ compiler and Windows Vista, 28 bytes of memory are allocated for a `string` object. This represents the size of the object.

Additional memory for the characters that make up the string might be allocated **dynamically** (as your program runs) when a value is stored in the `string` object. This is shown in Figure 6-2.

> **NOTE**
> 
> The amount of memory allocated for a string object may be different on your system.

```cpp
string cities[4];
cities[0] = "Chicago";
```

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_110_0.png)

**Figure 6-2** Memory allocation for `cities` array

In Figure 6-2, the compiler allocates enough consecutive memory locations to store four `string` objects for the array named `cities`. If the address of `cities[0]` is 1000, the address of `cities[1]` is 1028, and the address of `cities[3]` is 1084 because each string object requires 28 bytes of memory. When a string is assigned to `cities[0]`, memory is dynamically allocated at another memory address. This address is then stored in the array. When the statement `cities[0] = "Chicago";` executes, the memory dynamically allocated for Chicago begins at address 5000 and then that address (5000) is stored in the first element of the array. An example of creating `string` objects is presented later in this chapter.

> **NOTE**
> 
> Dynamic memory allocation is an advanced topic that you will learn more about when you take additional courses in C++ programming.

### INITIALIZING ARRAYS

In C++, array elements are not automatically initialized to any value when the array is declared. Therefore, all of the elements of an array contain a **garbage value**, which means they contain the values last stored at the memory location assigned to your array. Because these values are not useful in your program, it is a good idea to initialize arrays to all zeroes for arrays that store numbers and to empty strings for arrays that store strings. Two double quotes with no space between, `""`, is the empty string in C++.

> **NOTE**
> 
> When you initialize an array when you declare it, you do not specify the array's size within the square brackets. Instead, you use an empty pair of square brackets.

You can and will sometimes want to initialize arrays with values that you choose. You do this when you declare the array. To initialize an array when you declare it, use curly braces to surround a comma-delimited list of data items, as shown in the following example:

```cpp
int cityPopulations[] = {9500000, 871100, 23900, 40100};
string cities[] = {"Chicago", "Detroit", "Batavia", "Lima"};
```

> **NOTE**
> 
> These initializations create four elements for each array and assign values to them.

You can also use assignment statements to provide values for array elements after an array is declared, as in the following example:

```cpp
cityPopulations[0] = 9500000;
cities[0] = "Chicago";
```

A loop is often used to assign values to the elements in an array, as shown here:

```cpp
int loopIndex;
for(loopIndex = 0; loopIndex < 3; loopIndex++)
{
    cityPopulations[loopIndex] = 12345;
    cities[loopIndex] = "AnyCity";
}
```

The first time this loop is encountered, loopIndex is assigned the value 0. Because 0 is less than 3, the body of the loop executes, assigning the value 12345 to cityPopulations[0] and the value “AnyCity” to cities[0]. Next, the value of loopIndex is incremented and takes on the value 1. Because 1 is less than 3, the loop executes a second time and the value 12345 is assigned to cityPopulations[1] and “AnyCity” is assigned to cities[1]. Each time the loop executes, the value of loopIndex is incremented. This allows you to access a different location in the arrays each time the body of the loop executes.

> **NOTE**
> 
> Remember that subscript values begin with 0 (zero) in C++.

### ACCESSING ARRAY ELEMENTS

You need to access individual locations in an array when you assign a value to an array element, print its value, change its value, assign the value to another variable, and so forth. In C++, you use an integer expression placed in square brackets to indicate which element in the array you want to access. This integer expression is the subscript.

> **NOTE**
> 
> Later in this chapter, you will learn to use a named constant in an array declaration.

The following C++ program declares two arrays of data type double, initializes an array of data type double, copies values from one array to another, changes several values stored in the array named target, and prints the values of the arrays named source and target. You can compile and execute this program if you like. It is stored in the file named ArrayTest.cpp. Figure 6-3 shows the output generated by the ArrayTest program.

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
    double target[3];
    double source[] = {1.0, 5.5, 7.9};
    int loopIndex;
    // Copy values from source to target
    for(loopIndex = 0; loopIndex < 3; loopIndex++)
        target[loopIndex] = source[loopIndex];
    // Assign values to two elements of target
    target[0] = 2.0;
    target[1] = 4.5;
    // Print values stored in source and target
    for(loopIndex = 0; loopIndex < 3; loopIndex++)
    {
        cout << "Source " << source[loopIndex] << endl;
        cout << "Target " << target[loopIndex] << endl;
    }
}
```
