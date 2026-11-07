
## Creating vector Objects

Lines 11–12 create two vector objects that store values of type `int`—`integers1` contains seven elements, and `integers2` contains 10 elements. By default, each vector object’s elements are set to 0. Like arrays, vectors can store most data types—simply replace `int` in `std::vector<int>` with the appropriate type.

```cpp
10   int main() {
11       std::vector<int> integers1(7);  // 7-element vector<int>
12       std::vector<int> integers2(10); // 10-element vector<int>
13
```

Note that we used parentheses rather than a braced initializer to pass the size argument to each vector object’s constructor. When creating a vector, if the braces contain one value of the vector’s element type, the compiler treats the braces as a one-element initializer list rather than the vector’s size. So the following declaration actually creates a one-element vector<int> containing the value 7, not a seven-element vector:

```cpp
std::vector<int> integers1{7};
```

If you know the vector’s contents at compile-time, you can use an initializer list and class template argument deduction (CTAD) to define the vector, as we’ve done with arrays. For example, the following statement defines a four-element vector of doubles:

```cpp
std::vector integers1{1.1, 2.2, 3.3, 4.4};
```

## vector Member Function size; Function outputVector

Line 15 uses vector member function size to obtain integers1’s number of elements.⁸ Line 17 passes integers1 to function outputVector (lines 93–99), which displays the integers.

```cpp
14      // print integers1 size and contents
15      std::cout << "Size of vector integers1 is " << integers1.size()
16           << "\nvector after initialization:";
17      outputVector(integers1);
18
19      // print integers2 size and contents
20      std::cout << "\nSize of vector integers2 is " << integers2.size()
21           << "\nvector after initialization:";
22      outputVector(integers2);
23
```

```text
Size of vector integers1 is 7
vector after initialization: 0 0 0 0 0 0 0

Size of vector integers2 is 10
vector after initialization: 0 0 0 0 0 0 0 0 0 0
```

## Function inputVector

Lines 26–27 pass integers1 and integers2 to function inputVector (lines 102–106) to read values for each vector’s elements from the user.

```cpp
// input and print integers1 and integers2
std::cout << "\nEnter 17 integers:\n";
inputVector(integers1);
inputVector(integers2);

std::cout << "\nAfter input, the vectors contain:\n"
          << "integers1:";
outputVector(integers1);
std::cout << "integers2: ";
outputVector(integers2);
```

```text
Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the vectors contain:
integers1: 1 2 3 4 5 6 7
integers2: 8 9 10 11 12 13 14 15 16 17
```

## Comparing vector Objects for Inequality

In Chapter 5, we introduced function overloading. A similar concept is operator overloading, which allows you to define how a built-in operator works for a custom type. The C++ standard library defines overloaded operators == and != that compare two arrays or two vectors for equality or inequality, respectively. Line 38 compares two vector objects using the != operator, returning true if the contents of two vectors are not equal and false otherwise. Two vectors are not equal if they have different lengths or the elements at the same indexes are not equal.

```cpp
// use inequality (!=) operator with vector objects
std::cout << "\nEvaluating: integers1 != integers2\n";

if (integers1 != integers2) {
   std::cout << "integers1 and integers2 are not equal\n";
}
```

```text
Evaluating: integers1 != integers2
integers1 and integers2 are not equal
```

## Initializing One vector with the Contents of Another

You can initialize a new vector by copying the contents of an existing one. Line 44 creates a vector object integers3 and initializes it with a copy of integers1. Here, we used CTAD to infer integers3’s element type from that of integers1. Line 44 invokes the class template vector’s copy constructor to perform the copy operation. You’ll learn about copy constructors in detail in Chapter 11. Lines 46–48 output the size and contents of integers3 to demonstrate that it was initialized correctly.

```cpp
// create vector integers3 using integers1 as an
// initializer; print size and contents
std::vector integers3{integers1}; // copy constructor

std::cout << "\nSize of vector integers3 is " << integers3.size()
          << "\nVector after initialization: ";
outputVector(integers3);
```

```text
Size of vector integers3 is 7
vector after initialization: 1 2 3 4 5 6 7
```

## Assigning vectors and Comparing vectors for Equality

Line 52 assigns integers2 to integers1, demonstrating that the assignment (=) operator is overloaded to work with vector objects. Lines 54–57 output the contents of both objects to show that they now contain identical values. Line 62 then compares integers1 to integers2 with the equality (==) operator to determine whether the contents of the two objects are equal after the assignment, which they are.

```cpp
// use overloaded assignment (=) operator
std::cout << "\nAssigning integers2 to integers1:\n";
integers1 = integers2; // assign integers2 to integers1

std::cout << "\nintegers1: ";
outputVector(integers1);
std::cout << "\nintegers2: ";
outputVector(integers2);

// use equality (==) operator with vector objects
std::cout << "\nEvaluating: integers1 == integers2\n";

if (integers1 == integers2) {
    std::cout << "integers1 and integers2 are equal\n";
}
```

```text
Assigning integers2 to integers1:
integers1: 8 9 10 11 12 13 14 15 16 17
integers2: 8 9 10 11 12 13 14 15 16 17

Evaluating: integers1 == integers2
integers1 and integers2 are equal
```

## Using the at Member Function to Access and Modify vector Elements

Lines 67 and 71 use the vector member function at to obtain an element and use it to get a value from the vector and replace a value in the vector, respectively. If the index is valid, at returns either

- a reference to that element, which can be used to change the vector element’s value, or

## The try Statement

By default, an exception causes a C++ program to terminate. To handle an exception and possibly enable the program to continue executing, place any code that might throw an exception in a try statement (lines 76–82). The try block (lines 76–79) contains the code that might throw an exception, and the catch block (lines 80–82) contains the code that handles the exception if one occurs. The braces that delimit try and catch blocks' bodies are required. As you’ll see in Chapter 12, a single try block can have many catch blocks to handle different types of exceptions that might be thrown. If the code in the try block executes successfully, lines 80–82 are ignored.

## Executing the catch Block

When the program calls the vector member function at with the argument 15 (line 78), the function attempts to access the element at location 15, which is outside the vector’s bounds—integers1 has only 10 elements at this point. Bounds checking is performed at execution time, so at generates an exception. Specifically, line 78 throws an out_of_range exception (from header <stdexcept>) to notify the program of this problem. This immediately terminates the try block, skipping any remaining statements in that block. Then, the catch block begins executing. If you declared any variables in the try block, they’re now out of scope and not accessible to the catch block.

A catch block should declare its exception parameter (ex) as a const reference—we’ll say more about this in Chapter 12. The catch block can handle exceptions of the specified type. Inside the block, you can use the parameter’s identifier to interact with a caught exception object.

## The what Member Function of the Exception Object

When lines 80–82 catch the exception, the program displays a message (which varies by compiler) indicating the problem that occurred. Line 81 calls the exception object’s what member function to get the error message. Once the message is displayed in this example, the exception is considered handled, and the program continues with the next statement after the catch block’s closing brace. In this example, lines 85–89 execute next.

## Changing the Size of a vector

One key difference between a vector and an array is that a vector can dynamically grow and shrink as its number of elements varies. To demonstrate this, line 85 shows the current size of integers3, line 86 calls the vector’s push_back member function to add a new element containing 1000 to the end of the vector, and line 87 shows the new size of integers3. Line 89 then displays integers3’s new contents.

```cpp
// changing the size of a vector
std::cout << "\nCurrent integers3 size: " << integers3.size();
integers3.push_back(1000); // add 1000 to the end of the vector
std::cout << "\nNew integers3 size: " << integers3.size()
          << "\nintegers3 now contains: ";
outputVector(integers3);
}
```
