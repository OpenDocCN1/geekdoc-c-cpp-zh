
```
Current integers3 size is: 7
New integers3 size is: 8
integers3 now contains: 1 2 3 4 5 6 7 1000
```

### Functions outputVector and inputVector

Function outputVector uses a range-based for statement to obtain the value in each element of the vector for output. You could use a counter-controlled loop, but the range-based for is recommended. Similarly, function inputVector uses a range-based for statement with an int& range variable that can be used to store an input value in the corresponding vector element.

```cpp
// output vector contents
void outputVector(const std::vector<int>& items) {
    for (const int& item : items) {
        std::cout << item << ' ';
    }

    std::cout << '\n';
}

// input vector contents
void inputVector(std::vector<int>& items) {
    for (int& item : items) {
        std::cin >> item;
    }
}
```

### Straight-Line Code

As you worked through this chapter’s examples, you saw lots of for loops. You may have noticed in our Objects-Natural sections that much of the code that creates and uses objects is straight-line sequential code with few control statements. Working with objects often “flattens” code into lots of sequential function calls.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_354_0.png)

### Checkpoint

- 1. *(True/False)* The following declaration creates a seven-element `vector<int>`:
  
  `std::vector<int> integers1{7};`
  
  **Answer:** False. Actually, the declaration creates a one-element `vector<int>` containing the value 7, not a seven-element vector.

- 2. *(True/False)* When a try block throws an exception, this immediately terminates the try block, skipping any remaining statements in that block. Then, the catch block begins executing. If you declared any variables in the try block, they remain in scope and are accessible to the catch block.
  
  **Answer:** False. Actually, variables in the try block go out of scope and are not accessible to the catch block.

- 3. **(True/False)** A catch block should declare its exception parameter as a const reference. The catch block can handle exceptions of the specified type. Inside the block, you can use the parameter’s identifier to interact with a caught exception object.
  
  **Answer:** True.

## 6.16 Wrap-Up

This chapter began our introduction to data structures, using the C++ standard library class templates array and vector to store data in and retrieve data from lists and tables of values. We demonstrated how to declare an array, initialize an array and refer to individual elements of an array. We passed arrays to functions by reference and used the const qualifier to prevent the called function from modifying the array’s elements. You learned how to use the range-based for statement to manipulate every element of an array or a vector. We also demonstrated C++ standard library functions sort to sort an unsorted array and binary_search to search a sorted array.

You learned how to declare and manipulate two-dimensional arrays. We used nested counter-controlled and nested range-based for statements to iterate through all the rows and columns of a two-dimensional array. We also showed how to use auto to infer a variable’s type based on its initializer value. We introduced functional-style programming in C++ using C++20 ranges and views to compose lazy pipelines of operations.

In this chapter’s Objects-Natural case study, we demonstrated the capabilities of the C++ standard library class template vector. We discussed accessing array and vector elements with bounds checking and demonstrated basic exception-handling concepts. In later chapters, we’ll continue our coverage of data structures.

Chapter 7 presents one of C++’s most powerful features—the pointer. Pointers keep track of where data is stored in memory and enable us to manipulate those items in interesting ways. As you’ll see, C++ also provides a language element called an array (different from class template array) that’s closely related to pointers. In contemporary C++ code, it’s considered better practice to use the array class template rather than traditional arrays.

## Exercises

- 6.1 **(Fill in the Blanks)** Fill in the blanks in each of the following:
  
  - a) The names of the array p’s four elements are ______, ______, ______ and ______.
  - b) Naming an array, stating its type and specifying the number of elements in the array is called ______ the array.
  - c) When accessing an array element, by convention, the first subscript in a two-dimensional array identifies an element’s ______ and the second subscript identifies an element’s ______.
  - d) An *m-by-n* array contains ______ rows, ______ columns and ______ elements.
  - e) The name of the element in row 3 and column 5 of array d is ______.
  - f) ______ simplifies your code by enabling the compiler to infer (i.e., determine) an array’s element type from the values in its initializer list.
  - g) A(n) ______ processes a collection of values into a single value—this is one of the key operations in functional-style programming.
  - h) A(n) ______ receives another function as an argument.
  - i) A C++20 ______ is a collection of elements that you can iterate over.
  - j) The common functional-style programming operation known as ______ selects only those elements that match a condition.
  - k) The common functional-style programming operation known as ______ transforms a range’s values to new values, possibly of different types.

- 6.2 **(True or False)** Determine whether each of the following is *true* or *false*. If false, explain why.
  
  - a) To refer to a particular array element, we specify the array’s name and element’s value.
  - b) An array definition reserves space for an array.
  - c) To reserve 100 locations for integer array p, you write
    
    ```cpp
    p[100];
    ```
    
  - d) The only way to initialize all the elements of a 15-element array to zero is to use a loop that assigns zero to every element.
  - e) Functional-style programming emphasizes immutability, commonly performing operations that modify variables’ values.
  - f) The accumulate algorithm can be used to perform a reduction that totals the elements of an array.
  - g) Operations that generate values on-demand use lazy evaluation, which can reduce your program’s memory consumption and improve performance when all the values are not needed at once.
  - h) A view::range generates a range of integers from its first argument up to, but not including, its second argument.

- 6.3 **(Write C++ Statements)** Write C++ statements to accomplish each of the following:
  
  - a) Display the value of element 6 of the character array alphabet.
  - b) Input a value into element 4 of one-dimensional floating-point array grades.
  - c) Initialize each of the 5 elements of one-dimensional integer array values to 8.
  - d) Total and display the elements of array temperatures of 100 double elements.
  - e) Determine and display the smallest and largest values in array values containing 99 double elements.

- 6.4 **(One-Dimensional Array Questions)** Write statements that perform the following one-dimensional array operations:
  
  - a) Initialize the 10 elements of integer array counts to zero.
  - b) Add 1 to each of the 15 elements of integer array bonus.
  - c) Read 12 values for the array of doubles named monthlyTemperatures from the keyboard.
  - d) Print the 5 values of integer array bestScores.

- 6.5 **(Two-Dimensional Array Questions)** Consider a 2-by-3 integer array t.
  
  - a) Write a declaration for t.
  - b) How many rows does t have?
  - c) How many columns does t have?
  - d) How many elements does t have?
  - e) Write the names of all the elements in row 1 of t.
  - f) Write the names of all the elements in column 2 of `t`.
  - g) Write a statement that sets the element of `t` in row 0 and column 1 to zero.
  - h) Write a series of statements that initialize each element of `t` to zero. Do not use a loop.
  - i) Write a nested counter-controlled `for` statement that initializes each element of `t` to zero.
  - j) Write a nested range-based `for` statement that initializes each element of `t` to zero.
  - k) Write a statement that inputs the values for the elements of `t` from the keyboard.
  - l) Write a series of statements that determine and display the smallest value in array `t`.
  - m) Write a statement that displays the elements in row 0 of `t`.
  - n) Write a statement that totals the elements in column 2 of `t`.
  - o) Write a series of statements that prints the array `t` in neat, tabular format. List the column subscripts as headings across the top and list the row subscripts at the left of each row.

### 6.6 (Salesperson Salary Ranges)

Use a one-dimensional array to solve the following problem. A company pays its salespeople on a commission basis. The salespeople each receive $200 per week plus 9 percent of their weekly gross sales. For example, a salesperson who grosses $5000 in sales in a week receives $200 plus 9 percent of $5000, or a total of $650. Write a program (using an array of counters) that determines how many of the salespeople earned salaries in each of the following ranges (assume that each salesperson’s salary is truncated to an integer amount):

- a) $200–299
- b) $300–399
- c) $400–499
- d) $500–599
- e) $600–699
- f) $700–799
- g) $800–899
- h) $900–999
- i) $1000 and over

### 6.7 (Duplicate Elimination with array)

Use a one-dimensional array to solve the following problem. Read in 20 numbers, each of which is between 10 and 100, inclusive. As each number is read, validate it and store it in the array only if it isn’t a duplicate of a number already read. After reading all the values, display only the unique values that the user entered. Provide for the “worst case,” in which all 20 numbers are unique. Use the smallest possible array to solve this problem.

### 6.8 (Duplicate Elimination with vector)

Reimplement Exercise 6.7 using a vector. Begin with an empty vector and use its `push_back` function to add each unique value to the vector.

### 6.9 (Two-Dimensional array Initialization)

Label the elements of a 3-by-5 two-dimensional array `sales` to indicate the order in which they’re set to zero by the following program segment:
