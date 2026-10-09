In this example, the board is initialized and the size of each rank is explicitly identified. In addition to identifying the size as part of the new expression, the literal values for the array are provided. The literal values of type `bool[,]` are broken into two arrays of type `bool[,]`, size 3 × 3. Each two-dimensional array is composed of three `bool` arrays, size 3.

As already mentioned, each dimension in a multidimensional array must be consistently sized. However, it is also possible to define a **jagged array**, which is an array of arrays. Jagged array syntax is slightly different from that of a multidimensional array; furthermore, jagged arrays do not need to be consistently sized. Therefore, it is possible to initialize a jagged array as shown in Listing 3.17.

# LISTING 3.17: Initializing a Jagged Array

```
int[][] cells = { 
  new int[]{1, 0, 2, 0}, 
  new int[]{1, 2, 0}, 
  new int[]{1, 2}, 
  new int[]{1} 
};
```

A jagged array doesn't use a comma to identify a new dimension. Rather, a jagged array defines an array of arrays. In Listing 3.17, [] is placed after the data type int[], thereby declaring an array of type int[].

Notice that a jagged array requires an array instance (or null) for each internal array. In the preceding example, you use new to instantiate the internal element of the jagged arrays. Leaving out the instantiation would cause a compile error.

# Using an Array

You access a specific item in an array using the square bracket notation, known as the **array accessor**. To retrieve the first item from an array, you specify zero as the index. In Listing 3.18, the value of the fifth item (using the index 4 because the first item is index 0) in the languages variable is stored in the variable language.

# LISTING 3.18: Declaring and Accessing an Array

```
string[] languages = new string[9]{ 
 "C#", "COBOL", "Java", 
 "C++", "Visual Basic", "Pascal", 
 "Fortran", "Lisp", "J#"};
```