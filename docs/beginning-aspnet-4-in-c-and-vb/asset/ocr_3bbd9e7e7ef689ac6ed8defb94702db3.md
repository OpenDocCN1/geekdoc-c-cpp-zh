# 6

# Arrays and Tuples

# WHAT'S IN THIS CHAPTER?

+   - Simple arrays
+   - Multidimensional arrays
+   - Jagged arrays
+   - The Array class
+   - Arrays as parameters
+   - Enumerations
+   - Tuples
+   - Structural comparison

If you need to work with multiple objects of the same type, you can use collections (see Chapter 10) and arrays. C# has a special notation to declare, initialize, and use arrays. Behind the scenes, the Array class comes into play, which offers several methods to sort and filter the elements inside the array. Using an enumerator, you can iterate through all the elements of the array.

Also, .NET 4 introduces a new type Tuple that can be used to combine multiple objects of different types. See the “Tuples” section later in this chapter.

# SIMPLE ARRAYS

If you need to use multiple objects of the same type, you can use an array. An array is a data structure that contains a number of elements of the same type.

# Array Declaration

An array is declared by defining the type of elements inside the array followed by empty brackets and a variable name. For example, an array containing integer elements is declared as this:

```
int[] myArray;
```