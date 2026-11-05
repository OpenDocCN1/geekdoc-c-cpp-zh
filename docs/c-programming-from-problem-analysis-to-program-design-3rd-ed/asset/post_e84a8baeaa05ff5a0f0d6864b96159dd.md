
9. Using the following declaration:

```csharp
int[] x = { 12, 13, 14, 15, 16, 17, 18, 19 };
```

What does `x[8]` refer to?

- a. 19
- b. 18
- c. `\0`
- d. 0
- e. none of the above

10. Which of the following adds 42 to the element at the fifth physical spot?

```csharp
int[] x = { 12, 13, 14, 15, 16, 17, 18, 19 };
```

- a. `x[5] += 42;`
- b. `x[4] += 42;`
- c. `x[5 + 42];`
- d. `x = 42 + 5;`
- e. none of the above

11. How many components are allocated by the following statement?

```csharp
double[] values = new double[3];
```

- a. 32
- b. 3
- c. 2
- d. 4
- e. none of the above

12. What output is produced by the following code?

```csharp
int i;
int[] anArray = new int[5];
for (i = 0; i < anArray.Length; i++)
    anArray[i] = 2 * i;
for (i = 0; i < anArray.Length; i++)
    Console.Write(anArray[i] + " ");
```

- a. 2 2 2 2 2
- b. 2 4 6 8 10
- c. 0 2 4 6 8 10
- d. 0 2 4 6 8
- e. none of the above

13. If you declare an array as `int [ ] anArray = new int[5];` you can double the value stored in anArray [2] with the statement:

- a. `anArray [2] = anArray [5] * 2;`
- b. `anArray = anArray * 2;`
- c. `anArray [2] *= anArray [2] * 2;`
- d. `anArray [2] *= 2;`
- e. none of the above

14. With the following declaration:
`int [ ] points = {550, 700, 900, 800, 100};`
The statement `points [3] = points [3] + 10;` will

- a. replace the 800 amount with 810
- b. replace the 550 amount with 560
- c. replace the 900 amount with 910
- d. results in an error
- e. none of the above

15. With the following declaration:
`int [ ] points = {300, 100, 200, 400, 600};`
The statement `points [4] = points [4-2];` will

- a. replace the 400 amount with 2
- b. replace the 300 and 600 with 2
- c. replace the 600 with 200
- d. result in an error
- e. none of the above

16. With the following declaration:
`int [ ] points = {300, 100, 200, 400, 600};`
The statement `Console.Write(points [2] + points [3]);` will

- a. display 200400
- b. display 600
- c. display "points[2] + points[3]"
- d. result in an error
- e. none of the above

22. A valid call to the following method using a `params` parameter is:

```csharp
public static void DoSomething(params int[] item)
```

- a. `DoSomething(4);`
- b. `DoSomething(anArray);`
- c. `DoSomething(4, 5, 6);`
- d. a and c are correct
- e. all are correct

23. Using the following declaration:

```csharp
int [] anArray = {34, 55, 67, 89, 99};
```

What would be the result of each of the following output statements?

- a. `Console.WriteLine(anArray.Length);`
- b. `Console.WriteLine(anArray[2]);`
- c. `Console.WriteLine(anArray[anArray.Length -2]);`
- d. `Console.WriteLine(anArray[2 + 1] * anArray[0]);`
- e. `Console.WriteLine(anArray[1] + 100);`

24. Using the following declarations, write solutions for Steps a through e:

```csharp
int [] bArray = new int [10];
```

- a. Write a `foreach` loop to display the contents of bArray.
- b. Write a `for` loop to increment each element in bArray by 5.
- c. Use a member of the Array class to locate the index in the bArray array where 14 is stored.
- d. Use a member of the Array class to order the values in the bArray array.
- e. Use a member of the Array class to change the order of the elements in the bArray array. The contents of the first cell should hold what was in the last cell. The second cell should hold what was in the next to last cell.

25. Create array declarations for the following problem specifications.

- a. An array to hold the names of five font strings. Initialize the array with your favorites.
- b. An array to hold 12 state names. Initialize with the 12 states closest to your campus.
- c. An array to hold the 10 most common single character middle initials.
- d. An array to store a key for an exam consisting of 15 true/false questions.
- e. Parallel arrays to hold up to 100 checking account check numbers, dates, and check amounts.

26. Explain the difference between the pass by reference and pass by value. When an array is sent to a method, which one is used?

## Programming Exercises

- 1. Write a program that reads data into an array of type `int`. Valid values are from 0 to 10. Your program should determine how many values were inputted. Output a list of distinct entries and a count of how many times that entry occurred.

Use the following test data:

1  7  2  4  2  3  8  4  6  4  4  7

- 2. Write a program that accepts any number of integer input values. Total the values. Display a report showing the original value input and the percentage it contributes to the total. You may prompt the user for the number of values to be inputted.

- 3. Write a two class application that has a one-dimensional array as a data member. The array stores temperatures for any given week. Provide constructors for instantiating the class and methods to return the highest temperature, lowest temperature, average temperature, and the average temperature excluding the lowest temperature. Provide a method that accepts as an argument a temperature and returns the number of days the temperatures were below that value. Override the `ToString()` method to return the temperature range for the given week. Write a second class to test your class.

- 4. Create three arrays of type `double`. Do a compile-time initialization and place 10 different values in two of the arrays. Write a program to store the product of the two arrays in the third array. Produce a display using the `MessageBox` class that shows the contents of all three arrays using a single line for an element from all three arrays.

- 5. Write a program that allows the user to enter any number of names, last name first. Using one of the predefined methods of the Array class, order the names in ascending order. Display the results.

- 6. Write a two class application that has as a data member an array that can store state area codes. The class should also have a method that enables users to test an area code to determine if a number is one of the area codes in the state exchange. The method should use one of the predefined methods of the Array class and return `true` if the argument to the method is one of the state codes. Override the `ToString()` method to return the full list of area codes with each surrounded by parentheses. To test the class, store a list of state codes in a one-dimensional array. Send that array as an argument to the class.

- 7. Create an application that sorts a collection of integers and performs a binary search for one of the elements. Perform a compile-time initialization of your array with 15 unsorted values. Test your application by searching for values that do not exist in the array as well as values that are present.

- 8. Write a program that accepts 10 homework scores ranging in value from 0 through 10. Prompt the user for a new score if they enter a value out of the specified range. Store the values in an array. Calculate the average excluding the lowest and highest scores. Display the average as well as the highest and lowest scores that were discarded.

## 8

## Advanced Collections

In this chapter, you will:

- Create two dimensional arrays including rectangular and jagged types
- Use multidimensional arrays
- Use the `ArrayList class` to create dynamic lists
- Learn about the predefined methods of the `string class`
- Be introduced to the other collection classes
- Work through a programming example that illustrates the chapter’s concepts

In the last chapter, you were introduced to one-dimensional arrays. These are the basic data structure for many types of applications. In this chapter, you will discover how to work with other types of collections of data. In the last chapter you created parallel arrays that can hold multiple data values. In this chapter you will be introduced to members of the ArrayList class for creating collections that can grow and shrink. You will learn about special properties and methods of this class. You will also do additional programming using strings and learn about some of the predefined string methods available with the .NET Framework class library for accessing and modifying collections of character data items.

## Two-Dimensional Arrays

One-dimensional arrays are useful for storing lists of data. Because the data is stored in contiguous memory locations, elements are referenced by an index representing the location relative to the beginning element of the array. Two-dimensional and other multidimensional arrays follow the same guidelines you learned about with one-dimensional arrays. Two kinds of two-dimensional arrays can be created using C#. Rectangular is the first type, and this type is supported by most languages. The second type is called a jagged or ragged array. Two-dimensional arrays are referenced much like you reference a matrix.

## Rectangular Array

A rectangular two-dimensional array is usually visualized as a table divided into rows and columns. Much like a spreadsheet in which the rows and columns intersect, data is stored in individual cells. Figure 8-1 shows a table you might create to store calories consumed for a seven-day period. The table contains three columns and seven rows. Each cell holds one integer value.

![](img/e33ae760e23d89eac66541252ad65de8_447_0.png)

Figure 8-1 Two-dimensional structure
