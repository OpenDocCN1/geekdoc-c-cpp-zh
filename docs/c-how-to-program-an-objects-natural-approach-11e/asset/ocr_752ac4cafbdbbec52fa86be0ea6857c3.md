std::arrays—this is also true for built-in arrays. Of course, `std::array`’s `at` member function does bounds checking. Built-in arrays do not have a range-checked `at` indexing function, but you can use the Guidelines Support Library (GSL) function `gsl::at`, which receives as arguments the array and an index. This function’s first argument must be the array’s name, not a pointer to the array’s first element.

# Checkpoint

+   1. **(Code)** Write code to reserve seven elements for a built-in array of ints named `counts`.
+      **Answer:** `int counts[7];`
+   2. **(True/False)** The subscript (`[]`) operator does not provide bounds checking for `std::arrays` or built-in arrays.
+      **Answer:** True.
+   3. **(Fill-in)** `std::array`’s `_____` does bounds checking.
+      **Answer:** at member function.

# 7.5.2 Initializing Built-In Arrays

You can initialize the elements of a built-in array using an initializer list. For example,

```
int n[5]{50, 20, 30, 10, 40};
```

creates and initializes a built-in array of five ints. If you provide fewer initializers than the number of elements, the remaining elements are value initialized by default:

+   - fundamental numeric types are set to 0,
+   - bools are set to false,
+   - pointers are set to nullptr, and
+   - objects receive the default initialization specified by their class definitions (which we’ll discuss in Chapter 9).

If you provide too many initializers, a compilation error occurs.

The compiler can size a built-in array by counting its initializer list’s elements. For example, the following creates a five-element array:

```
int n[]{50, 20, 30, 10, 40};
```

# Checkpoint

+   1. **(Code)** Write code to initialize the four elements of built-in double array temperatures to 97.4, 99.1, 98.3 and 98.6.
+      **Answer:** `double temperatures[]{97.4, 99.1, 98.3, 98.6};`
+   2. **(True/False)** The following code will generate a compilation error:
+      ```cpp
+      int n[]{50, 20, 30};
+      ```
+      **Answer:** False. Even though the square brackets are empty, the compiler will infer that the built-in array’s size is 3, based on the number of initializers.