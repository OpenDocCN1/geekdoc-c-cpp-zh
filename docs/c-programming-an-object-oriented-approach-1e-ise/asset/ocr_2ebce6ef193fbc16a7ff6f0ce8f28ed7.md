**PRG-6.** Show how to call the *rand* function to create a random number that can only be 0 or 1 and simulates the tossing of a coin.

**PRG-7.** Show how to call the *rand* function to create a random number between 0.1 and 0.9 with only one digit after the decimal point. Hint: Find random numbers between 1 and 9 and then divide the result by 10 to get a double value. Write a program to test your answer with 10 numbers.

**PRG-8.** Show how to call the *rand* function to create a random number belonging to the following set: 2, 4, 6, 8, 10.

**PRG-9.** Write a program that prints the square root of the first 10 integers using the corresponding function in the `<cmath>` header. Tabulate your result with appropriate headers.

**PRG-10.** Write a program that prints the cubic root of the first 10 integers using the *pow* function in the `<cmath>` header. Tabulate your result with appropriate headers.

**PRG-11.** Write a function that finds \(\log_x\) using the log functions in the `<cmath>` header file. Note that we have \(\log_x = \log_b x / \log_b a\). Test your function in a program with values of \(x\) from 1 to 10. Tabulate your result with appropriate headers.

**PRG-12.** Write a function that, given a temperature in Celsius, returns the temperature in Fahrenheit. Use your function in a program and test it with Celsius values 0, 37, 40, and 100. The conversion from Celsius to Fahrenheit is given below:

\(\textbf{Fahrenheit} = \textbf{Celsius} * 180.0 / 100.0 + 32\)

**PRG-13.** Write a function that, given a temperature in Fahrenheit, returns the temperature in Celsius. Use your function in a program and test it with Fahrenheit values 32, 98.6, 104, and 212. The conversion from Fahrenheit to Celsius is given below:

\(\textbf{Celcius} = (\textbf{Fahrenheit} - 32) * (100.0 / 180.0)\)

**PRG-14.** Write a function to find the factorial of a positive number as shown below. Then use the function in a program to get the value of \(n\) from the user and print the factorial value. Test your program with values of \(n\) between 1 and 20 to avoid overflow.

\(\text{factorial}(n) = n * (n - 1) * (n - 2) * \ldots * 3 * 2 * 1\)

**PRG-15.** The permutation of \(n\) objects \(k\) at a time can be defined as shown below. The equation tells us how many permutations of \(n\) objects can be formed \(k\) elements at a time.

\(P(n, k) = \text{factorial}(n) / \text{factorial}(n - k)\)

**PRG-16.** The combination of \(n\) objects \(k\) at a time can be defined as shown below. The equation tells us how many combination of \(n\) objects can be formed \(k\) elements at a time.

\(P(n, k) = \text{factorial}(n) / (\text{factorial}(n - k) * \text{factorial}(k))\)

**PRG-17.** The Pascal triangle defines the coefficient of the terms \((C_n)\) in the expansion of the binomial

x + y)^n = C_0 x^0 y^n + C_1 x^1 y^{n-1} + ... + C_{n-1} x^{n-1} y^1 + C_n x^n y^0\)

The following shows the coefficient related to each \(n\) from 0 to 5. Note that both rows and columns start from 0.