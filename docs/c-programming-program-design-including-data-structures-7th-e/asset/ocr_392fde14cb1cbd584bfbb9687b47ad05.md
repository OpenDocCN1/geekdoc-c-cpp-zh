The algorithm for the program is:

+   1. Declare the variables.
+   2. Open the input and output files.
+   3. Initialize the variables.
+   4. While there is more data in the input file:
+      4.1. For each character in a line:
+         4.1.1. Read and write the character.
+         4.1.2. Increment the appropriate letter count.
+      4.2. Increment the line count.
+   5. Output the line count and letter counts.
+   6. Close the files.

To simplify the function `main`, we divide it into four functions:

+   - Function `initialize`
+   - Function `copyText`
+   - Function `characterCount`
+   - Function `writeTotal`

The following sections describe each of these functions in detail. Then, with the help of these functions, we describe the algorithm for the function `main`.

# initialize

This function initializes the variable `lineCount` and the array `letterCount` to 0. It, therefore, has two parameters: one corresponding to the variable `lineCount` and one corresponding to the array `letterCount`. Clearly, the parameter corresponding to `lineCount` must be a reference parameter. The definition of this function is:

```
```cpp
void initialize(int& lc, int list[])
{
    int j;
    lc = 0;

    for (j = 0; j < 26; j++)
        list[j] = 0;
} //end initialize
```
```

# copyText

This function reads a line and outputs the line. After reading a character, it calls the function `characterCount` to update the letter count. Clearly, this function has four parameters: an input file stream variable, an output file stream variable, a `char` variable, and the array to update the letter count.

Note that the `copyText` function does not perform the letter count, but we still pass the array `letterCount` to it. We take this step because this function calls the function `characterCount`, which needs the array `letterCount` to update the appropriate