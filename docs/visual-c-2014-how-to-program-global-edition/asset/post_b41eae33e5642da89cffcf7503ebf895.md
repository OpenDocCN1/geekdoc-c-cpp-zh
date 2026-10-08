
# Self-Review Exercises 393

- b) An array is a group of ______ (called elements) containing values that all have the same
- c) The ______ statement allows you to iterate through the elements in an array without using a counter.
- d) The number that refers to a primitive array is the element's ______.
- e) An array that uses indices is referred to as a(n) ______.
- f) Use the foreach header to iterate double array numbers.
- g) Use the expression ______ to receive the total number of arguments in a command line. Assume that command-line arguments are stored in args.
- i) Given the command MyApp test, the first command-line argument is
- j) A(n) ______ in the parameter of a method indicates that the method can receive a variable of arguments.
- k) As C# 6, you can declare ______ auto-implemented properties, which are read-only properties.

## 8.2 Determine which of the following is true or false. If false, explain why.

- a) A single array can store values of different types.
- b) An array index should normally be of type float.
- c) An individual array that's passed to a method and modified in that method will contain the modified value when the called method execution.
- d) Command-line arguments are separated by commas.
- e) Auto-implemented properties can be initialized in their declarations.

## 8.3 Perform the following tasks for an array called fractions:

- a) Declare ArraySize initialized to 10.
- b) Declare fractions which will reference an array with ArraySize elements of type double. Initialize the elements to 0.
- c) Name the element of the array with index 3.
- d) Assign the value 1.667 to the array element with index 9.
- e) Assign the value 3.333 to the array element with index 6.
- f) Sum all elements of the array, using a for statement. Declare integer variable x as a control variable for the loop.
- g) Sum all elements of the array, using a foreach statement. Declare double variable element as a control variable for the loop.

## 8.4 Perform the following tasks for an array called table:

- a) Declare and initialize it with a rectangular integer array that has three rows and columns. Assume constant ARRAY_SIZE has been declared to be 3.
- b) How many elements does the array contain?
- c) Use a nested statement to initialize each element of the array to the sum of its indices.

## 8.5 Find and correct the error in each of the following code segments:

```csharp
const int ArraySize = 5;
ArraySize = 10;
```

- b) Assume var b = new int[10];
for (var i = 0; i < b.Length; i++) {
  b[i] = 1;
}

- c) Assume int[,] a = {{1, 2}, {3, 4}};
a[1][1] = 5;

# Answers to Self-Review Exercises

- 8.1 a) arrays; variables, type c) foreach. d) two-dimension-alf) f) foreach (doubled in numbers). g) an array of strings, usually called args. h) args.length; i test. j) params modifier. k getter-only.

## 8.2 The answers to Self-Review Exercise 8.2 are:

- a) False. An array can store values of the same type.
- b) False. Array index must be an integer or an index.
- c) For individual value-type elements of an array False. A called method receives and ma-ipulates a copy of the value of such element, modifications do not affect the orig-inal value. If the reference of an array is passed to a method, modifications to t array elements in the called method are indeed reflected in the original. individual elements of an array type: True. A called method receives a copy of thenreference of such element, and changes to the referenced object will be reflected in the original element.
- d) False. Command-line arguments are separated by whitespace.
- e) As of C# 6, you can use-property initialization in auto-implemented prop-\erty declarations.

## 8.3 The answers to Self-Review Exercise 8.3 are:

```csharp
var total = 0.0;
foreach (var element in fractions)
{
    total += element;
}
```

## 8.4 The answers to Self-Review Exercise 8.4 are:

- a) var table = new int[ArraySize, ArraySize]
- b) Nine.
- c) for (var x = 0; x < table.GetLength(0)); ++x
{
    for (var y = 0; y < table.GetLength(1); ++y)
{
    table[x, y] = x + y;
}
```

## 8.5 The answers to Self-Review Exercise 8.5 are:

- a) Error: Assigning a value to a constant after it's been initialized.
Correction: Assign the correct value to the const declaration.
- b) Error: Referencing an array element outside the bounds of the array (b[10]).
Correction: Change the << operator to <.

- c) Error: Array indexing is performed incorrectly.
Correction: Change the statement to a[1, 1] = 5;

# Exercises

## 8.6 Fill in the blanks of the following statements:
- a) An exception object's ________ returns the exception's error message.
- b) Naming an array variable, stating its type and specifying the number of dimensions in the array is called ________ the array.
- c) In a two-dimensional array, the first index identifies the ________ of an element and the second index identifies the ________ of the element.
- d) C creates a value-length argument list a(n)
- e) The name of the element in row 3 and column 5 of jagged array d is

## 8.7 Determine whether each of the following is true or false. Explain why.
- a) To refer to a particular location or element within an array, we specify the name of the array's variable and the value of the particular element.
- b) Constants must be initialized when they are declared and cannot be modified.
- c) To indicate 100 locations should be reserved for integer array p, the programmer writes the
```csharp
p[100];
```
- d) The foreach statement iteration variable can be used only to access array elements, to modify them.
- e) To the elements of a two-dimensional array you must use.

## 8.8 Write statements to accomplish the following:
- a) Display the value of 6.
- b) Initialize the elements of 3.
- c) Total the elements of floating-point.
- d) Copy the one-dimensional array.
- e) Determine the smallest and largest.

## 8.9 Consider the three-dimensional array.
- a) Write a statement that declares t.
- b) How many rows does t have?
- c) How many columns does t have?
- d) How many elements does t have?
- e) List the names of t row 1.
- f) List the names of t column 2.
- g) Use a nested statement to set t to 0.
- h) Use a nested statement that inputs each of t.
- i) Use a nested statement that initializes t to 3.
- j) Use a nested statement to determine the elements of t.
- k) Use a statement to display the elements of t.
- l) Use a statement that displays t row 0.
- m) Use a statement that totals the elements of t.
- n) Write a statement that displays the elements in tabular format.

## 8.10 (Wages) Use a one-dimensional array to solve the following: A company pays its workers a fixed rate. Each die can show an integer value from 1 to 6, with 7 being the most frequent and 12 the least frequent sums. Fig 8.26 shows the 36 possible combinations of the two dice. Your app should roll the die 36,000 times. Use a one-dimensional array to tally the number of times each possible sum appears.

- a) $209
- b) $219
- c) $229
- d) $239
- e) $249
- f) $259
- g) $269
- h) $279
- i) $280

## 8.11 (Array Manipulations) Write statements that perform the following:
- a) Create a new object and assign its reference to an array.
- b) Display the contents of arrName using a foreach loop.
- c) Display the double values of arrPrice in color.

## 8.12 (Identifying Multiples of Eight) Use a one-dimensional array to solve the following: Write an app that inputs five numbers, each as an integer. Read and display only if it is a multiple of 8. Provide for the "worst case", which all five numbers are multiples of 8. Use the smallest array possible to solve this. Display the complete set of values after the user inputs each.

## 8.13 (Jagged Arrays) List the elements of the three-by-five array in the order which they're set to 0 by the following code:

```csharp
for (var row = 0; row < sales.Length; row++) {
  for (var col = 0; col < sales[row].Length; col++) {
    sales[row][col] = 0;
  }
}
```

## 8.14 (Variable-Length Argument List) Write an app that calculates the product of a series of integers that passed to method using a variable-length argument. Test your method with several calls, each with a different number of arguments.

## 8.15 (Command-Line Argument) Rewrite Fig 8.2 so that the array's size is specified by the first command-line argument. If no command-line argument is used, use 10 as the default value.

## 8.16 (Using the Statement) Write an app that uses a foreach statement to display the double values provided by the command-line arguments. [Hint: Use double parse to convert a string to a double.]

## 8.17 (Dice Rolling) Write an app to simulate the rolling of two dice. The app should use an object of class Random to roll the first die and again to roll the second die. The sum of the two values should be calculated. Each die can show an integer value from 1 to 6, with 7 being the most frequent and 12 the least frequent sums. Fig 8.26 shows the 36 possible combinations of the two dice. Your app should roll the die 36,000 times. Use a one-dimensional array to tally the number times each possible sum appears.
