
initializers. When initializing an array with an initializer list, if there are fewer initializers than elements in the array, the remaining elements are initialized to zero.

- If the array size is omitted from a declaration with an initializer list, the compiler determines the number of elements in the array by counting the number of elements in the initializer list.
- If the array size and an initializer list are specified in an array declaration, the number of initializers must be less than or equal to the array size.
- Constants must be initialized with a constant expression when they’re declared and cannot be modified thereafter. Constants can be placed anywhere a constant expression is expected.
- C++ has no array bounds checking. You should ensure that all array references remain within the bounds of the array.
- A static local variable in a function definition exists for the duration of the program but is visible only in the function body.
- A program initializes static local arrays when their declarations are first encountered. If a static array is not initialized explicitly by you, each element of that array is initialized to zero by the compiler when the array is created.

## Section 7.5 Passing Arrays to Functions

- To pass an array argument to a function, specify the name of the array without any brackets. To pass an element of an array to a function, use the subscripted name of the array element as an argument in the function call.
- Arrays are passed to functions by reference—the called functions can modify the element values in the callers’ original arrays. The value of the name of the array is the address in the computer’s memory of the first element of the array. Because starting address of the array is passed, the called function knows precisely where the array is stored in memory.
- Individual array elements are passed by value exactly as simple variables are. Such simple single pieces of data are called scalars or scalar quantities.
- To receive an array argument, a function’s parameter list must specify that the function expects to receive an array. The size of the array is not required between the array brackets.
- C++ provides the type qualifier const that can be used to prevent modification of array values in the caller by code in a called function. When an array parameter is preceded by the const qualifier, the elements of the array become constant in the function body, and any attempt to modify an element of the array in the function body results in a compilation error.

## Section 7.6 Case Study: Class GradeBook Using an Array to Store Grades

- Class variables (static data members) are shared by all objects of the class in which the variables are declared.
- A static data member can be accessed within the class definition and the member-function definitions like any other data member.
- A public static data member can also be accessed outside of the class, even when no objects of the class exist, using the class name followed by the binary scope resolution operator (::) and the name of the data member.

## Section 7.7 Searching Arrays with Linear Search

- The linear search compares each array element with a search key. Because the array is not in any particular order, it’s just as likely that the value will be found in the first element as the last. On average, a program must compare the search key with half the array elements. To determine that a value is not in the array, the program must compare the search key to every element in the array.

- scalable 290
- scalars 300
- scalar quantities 300
- search key 310
- searching 309
- size member function of vector 327
- sorting 311
- static data member 307
- structures 283
- subscript 284
- subscript 0 (zero) 284
- table of values 313
- two-dimensional arrays 313
- value of an element 284
- vector (C++ Standard Library class template) 323
- zeroth element 284

## Self-Review Exercises

### 7.1

Answer each of the following:

- a) Lists and tables of values can be stored in __________ or __________.
- b) The elements of an array are related by the fact that they have the same __________ and __________.
- c) The number used to refer to a particular element of an array is called its __________.
- d) A(n) __________ should be used to declare the size of an array, because it makes the program more scalable.
- e) The process of placing the elements of an array in order is called __________ the array.
- f) The process of determining if an array contains a particular key value is called __________ the array.
- g) An array that uses two subscripts is referred to as a(n) __________ array.

### 7.2

State whether the following are *true* or *false*. If the answer is *false*, explain why.

- a) An array can store many different types of values.
- b) An array subscript should normally be of data type float.
- c) If there are fewer initializers in an initializer list than the number of elements in the array, the remaining elements are initialized to the last value in the initializer list.
- d) It’s an error if an initializer list has more initializers than there are elements in the array.
- e) An individual array element that is passed to a function and modified in that function will contain the modified value when the called function completes execution.

### 7.3

Write one or more statements that perform the following tasks for an array called `fractions`:

- a) Define a constant integer variable `arraySize` initialized to 10.
- b) Declare an array with `arraySize` elements of type `double`, and initialize the elements to 0.
- c) Name the fourth element of the array.
- d) Refer to array element 4.
- e) Assign the value 1.667 to array element 9.
- f) Assign the value 3.333 to the seventh element of the array.
- g) Print array elements 6 and 9 with two digits of precision to the right of the decimal point, and show the output that is actually displayed on the screen.
- h) Print all the array elements using a for statement. Define the integer variable `i` as a control variable for the loop. Show the output.

### 7.4

Answer the following questions regarding an array called `table`:

- a) Declare the array to be an integer array and to have 3 rows and 3 columns. Assume that the constant variable `arraySize` has been defined to be 3.
- b) How many elements does the array contain?
- c) Use a for statement to initialize each element of the array to the sum of its subscripts. Assume that the integer variables `i` and `j` are declared as control variables.

- c) Initialize each of the 5 elements of one-dimensional integer array g to 8.
- d) Total and print the elements of floating-point array c of 100 elements.
- e) Copy array a into the first portion of array b. Assume double a[11], b[34];
- f) Determine and print the smallest and largest values contained in 99-element floating-point array w.

### 7.9

Consider a 2-by-3 integer array t.

- a) Write a declaration for t.
- b) How many rows does t have?
- c) How many columns does t have?
- d) How many elements does t have?
- e) Write the names of all the elements in row 1 of t.
- f) Write the names of all the elements in column 2 of t.
- g) Write a single statement that sets the element of t in the first row and second column to zero.
- h) Write a series of statements that initialize each element of t to zero. Do not use a loop.
- i) Write a nested for statement that initializes each element of t to zero.
- j) Write a statement that inputs the values for the elements of t from the keyboard.
- k) Write a series of statements that determine and print the smallest value in array t.
- l) Write a statement that displays the elements in row 0 of t.
- m) Write a statement that totals the elements in column 3 of t.
- n) Write a series of statements that prints the array t in neat, tabular format. List the column subscripts as headings across the top and list the row subscripts at the left of each row.

### 7.10 *(Salesperson Salary Ranges)*

Use a one-dimensional array to solve the following problem. A company pays its salespeople on a commission basis. The salespeople each receive $200 per week plus 9 percent of their gross sales for that week. For example, a salesperson who grosses $5000 in sales in a week receives $200 plus 9 percent of $5000, or a total of $650. Write a program (using an array of counters) that determines how many of the salespeople earned salaries in each of the following ranges (assume that each salesperson's salary is truncated to an integer amount):

- a) $200–299
- b) $300–399
- c) $400–499
- d) $500–599
- e) $600–699
- f) $700–799
- g) $800–899
- h) $900–999
- i) $1000 and over

### 7.11 *(Bubble Sort)*

In the bubble sort algorithm, smaller values gradually "bubble" their way upward to the top of the array like air bubbles rising in water, while the larger values sink to the bottom. The bubble sort makes several passes through the array. On each pass, successive pairs of elements are compared. If a pair is in increasing order (or the values are identical), we leave the values as they are. If a pair is in decreasing order, their values are swapped in the array. Write a program that sorts an array of 10 integers using bubble sort.

### 7.12 *(Bubble Sort Enhancements)*

The bubble sort described in Exercise 7.11 is inefficient for large arrays. Make the following simple modifications to improve the performance of the bubble sort:

- a) After the first pass, the largest number is guaranteed to be in the highest-numbered element of the array; after the second pass, the two highest numbers are "in place," and so on. Instead of making nine comparisons on every pass, modify the bubble sort to make eight comparisons on the second pass, seven on the third pass, and so on.
