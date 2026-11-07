```
```cpp
int counter;   //loop control variable
int number;    //variable to store the number read
int zeros;     //variable to store the zero count
int evens;     //variable to store the even count
int odds;      //variable to store the odd count
```
```

Clearly, you must initialize the variables zeros, evens, and odds to zero. You can initialize these variables when you declare them.

# MAIN ALGORITHM

+   1. Initialize the variables.
+   2. Prompt the user to enter 20 numbers.
+   3. For each number in the list:
+      a. Read the number.
+      b. Output the number (echo input).
+      c. If the number is even:
+         ```
+         {
+             i. Increment the even count.
+             ii. If the number is zero, increment the zero count.
+         }
+         otherwise
+             Increment the odd count.
+         ```
+   4. Print the results.

Before writing the C++ program, let us describe Steps 1–4 in greater detail. It will be much easier for you to then write the instructions in C++.

+   1. Initialize the variables. You can initialize the variables zeros, evens, and odds when you declare them.
+   2. Use an output statement to prompt the user to enter 20 numbers.
+   3. For Step 3, you can use a `for` loop to process and analyze the 20 numbers. In pseudocode, this step is written as follows:

```
```cpp
for (counter = 1; counter <= 20; counter++)
{
    read the number;
    output number;

    switch (number % 2)    // check the remainder
    {
    case 0:
        increment even count;
        if (number == 0)
            increment zero count;
        break;
```
```