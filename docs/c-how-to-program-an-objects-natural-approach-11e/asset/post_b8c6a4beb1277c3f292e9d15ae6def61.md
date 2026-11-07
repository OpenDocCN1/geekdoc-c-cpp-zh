
## 11.5.3 unique_ptr Ownership

Only one `unique_ptr` can own a dynamically allocated object, so assigning one `unique_ptr` to another transfers ownership to the target `unique_ptr`. The same is true when one `unique_ptr` is passed as an argument to another `unique_ptr`’s constructor. These operations use `unique_ptr`’s move assignment operator and move constructor, which we discuss in Section 11.6. **The last unique_ptr object that owns the dynamic memory will delete the memory. This makes unique_ptr an ideal mechanism for returning ownership of dynamically allocated objects to client code.**

## 11.5.4 unique_ptr to a Built-In Array

You can also use a `unique_ptr` to manage a dynamically allocated built-in array, as we’ll do in Section 11.6’s MyArray case study. For example, in the statement

```cpp
auto ptr{std::make_unique<int[]>(10)};
```

`make_unique`’s type argument is specified as `int[]`. So `make_unique` dynamically allocates a built-in array with the number of elements specified by its argument `(10)`. By default, the `int` elements are value initialized to `0`. The preceding statement uses `auto` to infer `ptr`’s type (`unique_ptr<int[]>`) from its initializer.

A `unique_ptr` that manages an array provides an **overloaded subscript operator (`[]`)** to access its elements. For example, the statement

```cpp
ptr[2] = 7;
```

assigns 7 to the `int` at `ptr[2]`, and the following statement displays that `int`:

```cpp
std::cout << ptr[2] << '\n';
```

### Checkpoint

- 1. *(Discussion)* Describe the strategy called RAII—Resource Acquisition Is Initialization for managing dynamically allocated resources like memory.
  - **Answer:** For any resource that must be returned to the system when the program is done using it, create the object as a local variable in a function—the object’s constructor should acquire the resource during object initialization. Next, use the object in your program. When the function call terminates, the object goes out of scope. At this point, the object’s destructor should release the resource.
- 2. *(Code)* Create a `unique_ptr` object and aim it at a new `std::string` object initialized with "hello":
  - **Answer:** `auto ptr{std::make_unique<std::string>("hello")};`
- 3. *(True/False)* Only one `unique_ptr` can own a dynamically allocated object, so assigning one `unique_ptr` to another is a compilation error.
  - **Answer:** False. Actually, assigning one `unique_ptr` to another transfers ownership to the target `unique_ptr`.

## 11.6 MyArray Case Study: Crafting a Valuable Class with Operator Overloading

Class development is an interesting, creative and intellectually challenging activity—always with the goal of crafting valuable classes. When we refer to “arrays” in this case study, we mean the built-in arrays discussed in Chapter 7. These pointer-based arrays have many problems, including:

- C++ does not check whether an array index is out-of-bounds. A program can easily “walk off” either end of an array, likely causing a fatal runtime error if you forget to test for this possibility in your code.
- Arrays of size *n* must use index values in the range 0 to *n* − 1. Alternative index ranges are not allowed.
- You cannot input an entire array with the stream extraction operator (`>>`) or output one with the stream insertion operator (`<<`). You must read or write every element.¹⁰
- Two arrays cannot be meaningfully compared with the equality or relational operators. Array names are simply pointers to where the arrays begin in memory. Two arrays will always be at different memory locations.
- When you pass an array to a general-purpose function that handles arrays of any size, you must pass the array’s size as an additional argument. As you saw in Section 7.10, C++20’s spans help solve this problem.
- You cannot assign one array to another with the assignment operator(s).

With C++, you can implement more robust array capabilities via classes and operator overloading, as has been done with C++ standard library class templates `array` and `vector`.

In this section, we’ll develop our own custom `MyArray` class that’s preferable to arrays. Internally, class `MyArray` will use a `unique_ptr` smart pointer to manage a dynamically allocated built-in array of `int` values.¹¹

We’ll create a powerful `MyArray` class with the following capabilities:

- `MyArray` objects perform range checking when you access them via the subscript (`[]`) operator to ensure indices remain within their bounds. Otherwise, the `MyArray` object will throw a standard library `out_of_range` exception.
- Entire `MyArray` objects can be input or output with the overloaded stream extraction (`>>`) and stream insertion (`<<`) operators without the client-code programmer having to write iteration statements.
- `MyArray` objects may be compared to one another with the equality operators `==` and `!=`. The class could easily be enhanced to include relational operators.
- `MyArray` objects know their own size, making it easier to pass them to functions.
- `MyArray` objects may be assigned to one another with the assignment operator.
- `MyArray` objects may be converted to `bool` (`false` or `true`) values to determine whether they are empty or contain elements.
- `MyArray` provides prefix and postfix increment (`++`) operators that add 1 to every element. We can easily add prefix and postfix decrement (`--`) operators.
- `MyArray` provides an addition assignment operator (`+=`) that adds a specified value to every element. The class could easily be enhanced to support the `-=`, `*=`, `/=`, and `%=` assignment operators.

Class `MyArray` will demonstrate the five special member functions and the `unique_ptr` smart pointer for managing dynamically allocated memory. We’ll use RAII (Resource Acquisition Is Initialization) throughout this example to manage the dynamically allocated memory resources. The class’s constructors will dynamically allocate memory as `MyArray` objects are initialized. The class’s destructor will deallocate the memory when the objects go out of scope, **preventing memory leaks**. Our `MyArray` class is not meant to replace standard library class templates `array` and `vector`, nor is it meant to mimic their capabilities. It demonstrates key C++ language and library features that you’ll find useful when you build your own classes.

### Checkpoint

- 1. *(True/False)* The contents of two pointer-based arrays can be meaningfully compared with equality or relational operators using the array names in an expression like

  ```cpp
  a1 == a2
  ```

  - **Answer:** False. Actually, they cannot. Array names are simply pointers to where the arrays begin in memory, so the preceding expression compares memory addresses of the arrays’ first elements.

### 11.6.1 Special Member Functions

Every class you define can have five special member functions, each of which we define in class `MyArray`:

- a copy constructor,
- a copy assignment operator,
- a move constructor,
- a move assignment operator and
- a destructor.

The copy constructor and copy assignment operator implement the class’s **copy semantics**—that is, how to copy a `MyArray` when it is passed by value to a function, returned by value from a function or assigned to another `MyArray`. The move constructor and move assignment operator implement the class’s **move semantics**, which eliminate costly, unnecessary copies of objects that are about to be destroyed. We discuss the details of these special member functions as we encounter the need for them throughout this case study.

### Checkpoint

- 1. *(True/False)* The copy constructor and copy assignment operator implement a class's copy semantics.
  - **Answer:** True.
- 2. *(Discussion)* What is the key advantage of using move semantics?
  - **Answer:** The move constructor and move assignment operator help eliminate costly unnecessary copies of objects that are about to be destroyed.

### 11.6.2 Using Class MyArray

The program of Figs. 11.3–11.5 demonstrates the `MyArray` class and its rich selection of overloaded operators. The code in Fig. 11.3 tests the various `MyArray` capabilities. We present the class definition in Fig. 11.4 and its member-function definitions in Fig. 11.5. We've broken the code and outputs into small segments for discussion purposes. For pedagogic purposes, many of class `MyArray`'s member functions, including all its special member functions, display output to show when they're called.

#### Function getArrayByValue

Later in this program, we'll call the `getArrayByValue` function (Fig. 11.3, lines 10–13) to create a local `MyArray` object by calling `MyArray`'s constructor that receives an initializer list. Function `getArrayByValue` returns that local object by value.

```cpp
1  // Fig11_03.cpp
2  // MyArray class test program.
3  #include <format>
4  #include <iostream>
5  #include <stdexcept>
6  #include <utility> // for std::move
7  #include "MyArray.h"
8
9  // function to return a MyArray by value
10 MyArray getArrayByValue() {
11    MyArray localInts{10, 20, 30}; // create three-element MyArray
12    return localInts; // return by value creates an rvalue
13 }
14
```

**Fig. 11.3** | MyArray class test program.

#### Creating MyArray Objects and Displaying Their Size and Contents

Lines 16–17 create objects `ints1` with seven elements and `ints2` with ten elements. Each calls the `MyArray` constructor that receives the number of elements and initializes the elements to zeros. Lines 20–21 display `ints1`'s size, then output its contents using `MyArray`'s overloaded stream insertion operator (`<<`). Lines 24–25 do the same for `ints2`.
