$E$ is the modulus of elasticity of the column's material.

$A$ is the cross-sectional area.

$L$ is the length of the column.

$r$ is the column's radius of gyration.

Using this formula, write a C++ function named `cLoad()` that accepts values of $E, A, L$, and $r$ and returns the critical buckling load.

+   b. Include the function written in Exercise 10a in a working program. Make sure your function is called from `main()` and returns a value to `main()` correctly. Have `main()` use a `cout` statement to display the returned value. Test the function by passing various data to it.

+   11. (Numerical) a. The following is an excellent programming algorithm for rounding a real number to $n$ decimal places:

+   Step 1: Multiply the number by $10^n$
Step 2: Add 0.5
Step 3: Delete the fractional part of the result
Step 4: Divide by $10^n$

For example, using this algorithm to round the number 78.374625 to three decimal places yields:

+   Step 1: $78.374625 \times 10^3 = 78374.625
Step 2: $78374.625 + 0.5 = 78375.125
Step 3: Retaining the integer part = $78375
Step 4: $78375$ divided by $10^3 = 78.375$

Using this, write a C++ function that accepts a user-entered value and returns the result to two decimal places.

+   b. Enter, compile and execute the program for Exercise 11a.

+   12. (Numerical) a. Write a C++ function named `whole()` that returns the integer of any number passed to it. *Hint*: Use the argument passed to the integer variable.

+   b. Include the function written in Exercise 12a in a working program. Make sure your function is called from `main()` and returns a value to `main()` correctly. Have `main()` use a `cout` statement to display the returned value. Test the function by passing various data to it.

+   13. (Numerical) a. Write a C++ function named `fracpart()` that returns the fractional part of any number passed to it. For example, if number 25.56879 is passed to `fracpart()`, the number 0.8979 is returned. Call the `whole()` function you wrote in Exercise 12. The number returned can then be determined as the number passed to `fracpart()` is the returned value when the same argument is passed to `whole()`. The completed program should consist of `main()` followed by `fracpart()` followed by `whole()`

+   b. Include the function written in Exercise 13a in a working program. Make sure your function is called from `main()` and returns a value to `main()` correctly. Have `main()` use a `cout` statement to display the returned value. Test the function by passing various data to it.