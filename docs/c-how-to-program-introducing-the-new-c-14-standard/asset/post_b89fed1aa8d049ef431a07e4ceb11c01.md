
## Section 7.5 Range-Based `for` Statement

- The new C++11 **range-based `for` statement** (p. 298) allows you to manipulate all the elements of an `array` without using a counter, thus avoiding the possibility of “stepping outside” the `array` and eliminating the need for you to implement your own bounds checking.
- A range-based `for` statement’s header contains a range variable declaration to the left of the colon and the name of a container to the right, as in

  ```cpp
  for (rangeVariableDeclaration : container)
  {
  }
  ```

- The range variable represents successive elements on successive iterations of the loop.
- You can use the range-based `for` statement with most of the C++ Standard Library’s prebuilt data structures (commonly called containers).
- You can use a range-based `for` statement to modify each element by making the range variable a reference.
- The range-based `for` statement can be used in place of the counter-controlled `for` statement whenever code looping through an `array` does not require access to the element’s subscript.

## Section 7.6 Case Study: Class `GradeBook`
### Using an `array` to Store Grades

- **Class variables (`static` data members; p. 304)** are shared by all objects of the class in which the variables are declared.
- A `static` data member can be accessed within the class definition and the member-function definitions like any other data member.
- A `public static` data member can also be accessed outside of the class, even when no objects of the class exist, using the class name followed by the scope resolution operator (`::`) and the name of the data member.

## Section 7.7 Sorting and Searching `arrays`

- Sorting data—placing it into ascending or descending order—is one of the most important computing applications.
- The process of finding a particular element of an `array` is called searching.
- C++ Standard Library function `sort` sorts an `array`’s elements into ascending order. The function’s arguments specify the range of elements that should be sorted. You’ll see that function `sort` can be used on other types of containers too.
- C++ Standard Library function `binary_search` determines whether a value is in an `array`. The sequence of values must be sorted in ascending order first. The function’s first two arguments represent the range of elements to search and the third is the search key—the value to locate. The function returns a `bool` indicating whether the value was found.

## Section 7.8 Multidimensional arrays

- **Multidimensional arrays** (p. 308) with two dimensions are often used to represent tables of values (p. 307) consisting of information arranged in rows and columns.
- Arrays that require two subscripts to identify a particular element are called two-dimensional arrays (p. 308). An array with *m* rows and *n* columns is called an *m*-by-*n* array (p. 308).

## Section 7.9 Case Study: Class `GradeBook`
### Using a Two-Dimensional `array`

- In a variable declaration, the **keyword** `auto` (p. 309) can be used in place of a type name to infer the variable’s type based on the variable’s initializer value.

## Section 7.10 Introduction to C++ Standard Library Class Template `vector`

- C++ Standard Library **class template** `vector` (p. 317) is similar to `array` but also supports resizing.
- By default, all the elements of an integer `vector` object are set to 0.
- A `vector` can be defined to store any data type using a declaration of the form

  ```cpp
  vector<type> name(size);
  ```

- **Member function** `size` (p. 320) of class template `vector` returns the number of elements in the `vector` on which it’s invoked.
- The value of an element of a `vector` can be accessed or modified using square brackets (`[]`).
- Objects of standard class template `vector` can be compared directly with the equality (`==`) and inequality (`!=`) operators. The assignment (`=`) operator can also be used with `vector` objects.
- A nonmodifiable *lvalue* (a `const` reference) is an expression that identifies an object in memory (such as an element in a vector), but cannot be used to modify that object. A modifiable *lvalue* (a non-`const` reference) also identifies an object in memory, but can be used to modify the object.
- An **exception** (p. 321) indicates a problem that occurs while a program executes. The name “exception” suggests that the problem occurs infrequently—if the “rule” is that a statement normally executes correctly, then the problem represents the “exception to the rule.”
- **Exception handling** (p. 321) enables you to create **fault-tolerant programs** (p. 321) that can resolve exceptions.
- To handle an exception, place the code that might **throw an exception** (p. 322) in a `try` statement.
- The `try` **block** (p. 322) contains the code that might throw an exception, and the `catch` **block** (p. 322) contains the code that handles the exception if one occurs.
- When a `try` block terminates, any variables declared in the `try` block go out of scope.
- A `catch` block declares a type and an exception parameter. Inside the `catch` block, you can use the parameter’s identifier to interact with a caught exception object.
- An exception object’s `what` **member function** (p. 322) returns the exception’s error message.

## Self-Review Exercises

- **7.1 (Fill in the Blanks)** Answer each of the following:
  - A. Lists and tables of values can be stored in ______ or ______.
  - B. An `array`’s elements are related by the fact that they have the same ______ and ______.
  - C. The number used to refer to a particular element of an `array` is called its ______.
  - D. A(n) ______ should be used to declare the size of an `array`, because it eliminates magic numbers.
  - E. The process of placing the elements of an `array` in order is called ______ the `array`.
  - F. The process of determining if an `array` contains a particular key value is called ______ the `array`.
  - G. An `array` that uses two subscripts is referred to as a(n) ______ `array`.

- **7.2 (True or False)** State whether the following are *true* or *false*. If the answer is false, explain why.
  - A. A given `array` can store many different types of values.
  - B. An `array` subscript should normally be of data type `float`.
  - C. If there are fewer initializers in an initializer list than the number of elements in the `array`, the remaining elements are initialized to the last value in the initializer list.
  - D. It’s an error if an initializer list has more initializers than there are elements in the `array`.

- **7.3 (Write C++ Statements)** Write one or more statements that perform the following tasks for an `array` called `fractions`:
  - A. Define a constant variable `arraySize` to represent the size of an `array` and initialize it to `10`.
  - B. Declare an `array` with `arraySize` elements of type `double`, and initialize the elements to `0`.
  - C. Name the fourth element of the `array`.
  - D. Refer to `array` element 4.
  - E. Assign the value `1.667` to `array` element 9.
  - F. Assign the value `3.333` to the seventh element of the `array`.
  - G. Display `array` elements 6 and 9 with two digits of precision to the right of the decimal point, and show the output that’s actually displayed on the screen.
  - H. Display all the `array` elements using a counter-controlled `for` statement. Define the integer variable `i` as a control variable for the loop. Show the output.
  - I. Display all the `array` elements separated by spaces using a range-based `for` statement.

- **7.4 (Two-Dimensional `array` Questions)** Answer the following questions regarding a two-dimensional `array` called `table`:
  - A. Declare the `array` to store `int` values and to have 3 rows and 3 columns. Assume that the constant variable `arraySize` has been defined to be 3.
  - B. How many elements does the `array` contain?
  - C. Use a counter-controlled `for` statement to initialize each element of the `array` to the sum of its subscripts.
  - D. Write a nested `for` statement that displays the values of each element of `array` `table` in tabular format with 3 rows and 3 columns. Each row and column should be labeled with the row or column number. Assume that the `array` was initialized with an initializer list containing the values from 1 through 9 in order. Show the output.

- **7.5 (Find the Error)** Find and correct the error in each of the following program segments:
  - A. `#include <iostream>;`
  - B. `arraySize = 10; // arraySize was declared const`
  - C. Assume that `array<int, 10> b;`

    ```cpp
    {
        for (size_t i{0}; i <= b.size(); ++i) {
            b[i] = 1;
        }
    }
    ```
