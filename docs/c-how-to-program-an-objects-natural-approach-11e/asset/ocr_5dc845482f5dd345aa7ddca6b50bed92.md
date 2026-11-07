# 7.5.3 Passing Built-In Arrays to Functions

The value of a built-in array’s name is implicitly convertible to a pointer to the array’s first element. This is known as decaying to a pointer. Given the array

```
int n[]{50, 20, 30, 10, 40};
```

the name n is implicitly convertible to &n[0], which is a pointer to the element containing 50. You don’t need to take a built-in array’s address (&) to pass it to a function—just pass its name. As you saw in Section 7.4, a function that receives a pointer to a variable in the caller can modify that variable in the caller. For built-in arrays, the called function can modify all of the array’s elements in the caller—unless the parameter is declared const to prevent the argument array in the caller from being modified (discussed in Section 7.7).

# Checkpoint

+   1. **(True/False)** You must take a built-in array’s address (&) to pass it to a function.  
+      **Answer:** False. You can just pass the array’s name, which decays to a pointer to the array’s first element.
+   
+   2. **(Fill-in)** A function that receives a pointer to a built-in array variable in the caller can modify that array in the caller unless the parameter is declared ________.  
+      **Answer:** const.

# 7.5.4 Declaring Built-In Array Parameters

You can declare a built-in array parameter in a function header as follows:

```
int sumElements(const int values[], size_t numberOfElements)
```

Here, the function’s first argument should be a one-dimensional built-in array of const ints. Unlike std::arrays and std::vectors, built-in arrays don’t know their own size, so a function that processes a built-in array also should receive the built-in array’s size.

The preceding header also can be written as

```
int sumElements(const int* values, size_t numberOfElements)
```

The compiler does not differentiate between a function that receives a pointer and one that receives a built-in array. In fact, the compiler converts const int values[] to const int* values under the hood. This means the function must “know” when it’s receiving a pointer to a built-in array’s first element vs. a single variable being passed by reference.

> The C++ Core Guidelines say not to pass built-in arrays to functions as just a pointer. Instead, you should pass C++20 spans because they maintain a pointer to the array’s first element and the array’s size. In Section 7.10, we’ll demonstrate spans, and you’ll see that passing a span is superior to passing a built-in array and its size to a function.

# Checkpoint

+   1. **(True/False)** Built-in arrays don’t know their own size, so a function that processes a built-in array also should receive its size.  
+      **Answer:** True.

9. C++ Core Guidelines, “I.13: Do not pass an array as a single pointer.” Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#slcon-arrays