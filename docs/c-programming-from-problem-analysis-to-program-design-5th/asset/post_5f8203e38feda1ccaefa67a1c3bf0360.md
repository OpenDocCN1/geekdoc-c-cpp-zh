
- **17.** To design a recursive function, you must do the following:
  - a. Understand the problem requirements.
  - b. Determine the limiting conditions. For example, for a list, the limiting condition is the number of elements in the list.
  - c. Identify the base cases and provide a direct solution to each base case.
  - d. Identify the general cases and provide a solution to each general case in terms of smaller versions of itself.

## EXERCISES

- **1.** Mark the following statements as true or false.
  - a. Every recursive definition must have one or more base cases.
  - b. Every recursive function must have one or more base cases.
  - c. The general case stops the recursion.
  - d. In the general case, the solution to the problem is obtained directly.
  - e. A recursive function always returns a value.

- **2.** What is a base case?

- **3.** What is a recursive case?

- **4.** What is direct recursion?

- **5.** What is indirect recursion?

- **6.** What is tail recursion?

- **7.** Consider the following recursive function:

```cpp
int mystery(int number)                         //Line 1
{
    if (number == 0)                             //Line 2
        return number;                           //Line 3
    else                                         //Line 4
        return (number + mystery(number - 1));   //Line 5
}
```

  - a. Identify the base case.
  - b. Identify the general case.
  - c. What valid values can be passed as parameters to the function mystery?
  - d. If mystery(0) is a valid call, what is its value? If not, explain why.
  - e. If mystery(5) is a valid call, what is its value? If not, explain why.
  - f. If mystery(-3) is a valid call, what is its value? If not, explain why.

- **8.** Consider the following recursive function:

```cpp
void funcRec(int u, char v)                     //Line 1
{
    if (u == 0)                                  //Line 2
        cout << v;                               //Line 3
    else if (u == 1)
        cout << static_cast<char>(static_cast<int>(v) + 1);  //Line 4
    else                                         //Line 6
        funcRec(u - 1, v);                       //Line 7
}
```

Answer the following questions:

  - a. Identify the base case.
  - b. Identify the general case.
  - c. What is the output of the following statement? `funcRec(5, 'A');`

- **9.** Consider the following recursive function:

```cpp
void recFun(int x)
{
    if (x > 10)
    {
        recFun(x / 10);
        cout << x % 10 << endl;
    }
    else
        cout << x << endl;
}
```

What is the output of the following statements?

  - a. `recFun(258);`
  - b. `recFun(7);`
  - c. `recFun(36);`
  - d. `recFun(-85);`

- **10.** Consider the following recursive function:

```cpp
void recFun(int u)
{
    if (u == 1)
        cout << "Stop! ";
    else
    {
        cout << "Go ";
        recFun(u - 1);
    }
}
```

What is the output, if any, of the following statements?

  - a. `recFun(7);`
  - b. `recFun(3);`
  - c. `recFun(-6);`

- **11.** Consider the following recursive function:

```cpp
void exercise(int x)
{
    if (x > 0 && x < 10)
    {
        cout << x << " ";
        exercise(x + 1);
    }
}
```

What is the output of the following statements?

  - a. `exercise(0);`
  - b. `exercise(5);`
  - c. `exercise(10);`
  - d. `exercise(-5);`

- **12.** Consider the following function:

```cpp
int test(int x, int y)
{
    if (x == y)
        return x;
    else if (x > y)
        return (x + y);
    else
        return test(x + 1, y - 1);
}
```

What is the output of the following statements?

  - a. `cout << test(5, 10) << endl;`
  - b. `cout << test(3, 9) << endl;`

- **13.** Consider the following function:

```cpp
int func(int x)
{
    if (x == 0)
        return 2;
    else if (x == 1)
        return 3;
    else
        return (func(x - 1) + func(x - 2));
}
```

What is the output of the following statements?

  - a. `cout << func(0) << endl;`
  - b. `cout << func(1) << endl;`
  - c. `cout << func(2) << endl;`
  - d. `cout << func(5) << endl;`

- **14.** Suppose that `intArray` is an array of integers, and `length` specifies the number of elements in `intArray`. Also, suppose that `low` and `high` are two integers such that `0 <= low < length`, `0 <= high < length`, and `low < high`. That is, `low` and `high` are two indices in `intArray`. Write a recursive definition that reverses the elements in `intArray` between `low` and `high`.

- **15.** Write a recursive algorithm to multiply two positive integers `m` and `n` using repeated addition. Specify the base and the recursive case.

- **16.** Consider the following problem: How many ways can a committee of four people be selected from a group of 10 people? There are many other similar problems in which you are asked to find the number of ways to select a set of items from a given set of items. The general problem can be stated as follows: Find the number of ways *r* different things can be chosen from a set of *n* items, in which *r* and *n* are nonnegative integers and *r* ≤ *n*. Suppose *C*(*n*, *r*) denotes the number of ways *r* different things can be chosen from a set of *n* items. Then, *C*(*n*, *r*) is given by the following formula:

  \[
  C(n, r) = \frac{n!}{r!(n-r)!}
  \]

  in which the exclamation point denotes the factorial function. Moreover, *C*(*n*, 0) = *C*(*n*, *n*) = 1. It is also known that *C*(*n*, *r*) = *C*(*n* − 1, *r* − 1) + *C*(*n* − 1, *r*).

  - a. Write a recursive algorithm to determine *C*(*n*, *r*). Identify the base case(s) and the general case(s).
  - b. Using your recursive algorithm, determine *C*(5, 3) and *C*(9, 4).

### PROGRAMMING EXERCISES

- **1.** Write a recursive function that takes as a parameter a nonnegative integer and generates the following pattern of stars. If the nonnegative integer is 4, then the pattern generated is:

```
****
***
**
*
*
**
***
****
```

Also, write a program that prompts the user to enter the number of lines in the pattern and uses the recursive function to generate the pattern. For example, specifying 4 as the number of lines generates the above pattern.

- **2.** Write a recursive function to generate a pattern of stars, such as the following:

```
*
**
***
****
*****
****
***
**
*
```

Also, write a program that prompts the user to enter the number of lines in the pattern and uses the recursive function to generate the pattern. For example, specifying 4 as the number of lines generates the above pattern.

- **3.** Write a recursive function to generate the following pattern of stars:

```
    *
   * *
  * * *
 * * * *
  * * *
   * *
    *
```

Also, write a program that prompts the user to enter the number of lines in the pattern and uses the recursive function to generate the pattern. For example, specifying 4 as the number of lines generates the above pattern.

- **4.** Write a recursive function, vowels, that returns the number of vowels in a string. Also, write a program to test your function.

- **5.** Write a recursive function named `sumSquares` that returns the sum of the squares of the numbers from 0 to num, in which num is a nonnegative `int` variable. Do not use global variables; use the appropriate parameters. Also write a program to test your function.

- **6.** Write a recursive function that finds and returns the sum of the elements of an `int` array. Also, write a program to test your function.

- **7.** A palindrome is a string that reads the same both forward and backward. For example, the string "madam" is a palindrome. Write a program that uses a recursive function to check whether a string is a palindrome. Your program must contain a value-returning recursive function that returns `true` if the string is a palindrome and `false` otherwise. Do not use any global variables; use the appropriate parameters.

- **8.** Write a program that uses a recursive function to print a string backward. Do not use any global variables; use the appropriate parameters.

- **9.** Write a recursive function, `reverseDigits`, that takes an integer as a parameter and returns the number with the digits reversed. Also, write a program to test your function.

- **10.** Write a recursive function, `power`, that takes as parameters two integers x and y such that x is nonzero and returns xʸ. You can use the following recursive definition to calculate xʸ. If y ≥ 0:

$$
power(x,y)=\begin{cases}
1 & \text{if } y=0\\
x & \text{if } y=1\\
x\times power(x,y-1) & \text{if } y>1
\end{cases}
$$
