
```cpp
}
else if (num == 2)
{
    return true;
}
return isPrime(2, num);
}
```

Note that after taking care of the two special cases, the nonrecursive function calls the recursive function with divisor 2 to start. Program 17.12 shows the complete program using the two functions.

## Program 17.12 Testing the primeness of an integer

```cpp
/********************************************************
 * A program to test the primeness of an integer        *
 ********************************************************/
#include <iostream>
#include <cmath>
using namespace std;

// Declaration of a non-recursive and a recursive function
bool isPrime(int num);
bool isPrime(int div, int num);

int main( )
{
    // Testing the primeness of some integers
    cout << "Is 1 prime?  " << boolalpha << isPrime(1) << endl;
    cout << "Is 2 prime?  " << boolalpha << isPrime(2) << endl;
    cout << "Is 7 prime?  " << boolalpha << isPrime(7) << endl;
    cout << "Is 21 prime? " << boolalpha << isPrime(21) << endl;
    cout << "Is 59 prime? " << boolalpha << isPrime(59) << endl;
    cout << "Is 97 prime? " << boolalpha << isPrime(97) << endl;
    cout << "Is 301 prime?" << boolalpha << isPrime(301) << endl;
    return 0;
}
// Definition of non-recursive function calling the recursive function
bool isPrime(int num)
{
    if (num <= 1)
    {
        return false;
    }
    else if (num == 2)
    {
        return true;
    }
    return isPrime(2, num);
}
// Definition of the recursive (helper) function
bool isPrime(int div, int num)
{
    if (num % div == 0)
    {
        return false;
    }
    else if (div >= floor(sqrt(num)))
    {
        return true;
    }
    return isPrime(div + 1, num);
}
```

Run:

```text
Is 1 prime? false
Is 2 prime? true
Is 7 prime? true
Is 21 prime? false
Is 59 prime? true
Is 97 prime? true
Is 301 prime? false
```

## Key Terms

- base case
- binary search
- general case
- helper function
- nontail recursion
- Sort
- tail recursion

## Summary

We can solve an iteration problem using either repetition or recursion. In repetition, we let a function repeat itself until a terminating condition occurs. In recursion, we let a function call itself until the same terminating condition occurs.

We have two types of recursion: tail recursion and nontail recursion. Tail recursion is normally more efficient and uses less computer resources than nontail recursion. We can change a nontail recursion to a tail recursion by defining more parameters.

Two areas in which we encounter recursion are sorting and searching a list such as an array of items.

The Towers of Hanoi is a classical recursive algorithm that uses many aspects of recursion.

## Problems

- **PR-1.** What is printed from *fun*('G') as coded below? Explain what the function does.

```cpp
void fun (char c)
{
    if (c < 'A' || c > 'Z')
    {
        return;
    }
    cout << c << " ";
    fun (c + 1);
}
```

- **PR-2.** What is returned from *fun*(5, 12) and *fun*(12, 5) as coded below? Explain what the function does.

```cpp
int fun (int n, int m)
{
    if (n == m)
    {
        return 0;
    }
    else if (n > m)
    {
        return 1;
    }
    else
    {
        return fun (m, n);
    }
}
```

- **PR-3.** What is printed from *fun*(5) as coded below? Explain what the function does.

```cpp
void fun (int n)
{
    if (n < 0)
    {
        return;
    }
    cout << n << " ";
    fun (n - 1);
}
```

- **PR-4.** What is returned from *fun*(5) as coded below? Explain what the function does.

```cpp
double fun (int n)
{
    if (n <= 1)
    {
        return 0;
    }
    return fun (n - 1) + 1.0 / n;
}
```

- **PR-5.** What is returned from *fun(4)* as coded below? Explain what the function does.

```cpp
double fun (int n)
{
    if (n <= 1)
    {
        return 0;
    }
    return fun (n - 1) + double (n) / (n + 2);
}
```

- **PR-6.** What is returned from *fun(4)* as coded below? Explain what the function does.

```cpp
double fun (int n)
{
    if (n <= 1)
    {
        return 0;
    }
    return fun (n - 1) + double (n) / (2 * n - 1);
}
```

- **PR-7.** What is returned from *fun(4)* as coded below? Explain what the function does.

```cpp
double fun (int n)
{
    if (n <= 1)
    {
        return 0;
    }
    return fun (n - 1) + double (n) / (3 * n - 1);
}
```

- **PR-8.** What is printed from *fun(164)* as coded below? Explain what the function does.

```cpp
int fun (int n)
{
    if (n < 10)
    {
        return n;
    }
    else
    {
        cout << (n % 10);
        return fun (n / 10);
    }
}
```

- **PR-9.** Explain what the following function does and what is returned when *n* is 3 and *m* is 4.

```cpp
int fun (int n, int m)
{
    if (n == 0 || m == 0)
    {
        return 1;
    }
    else
    {
        return fun(n, m - 1) + fun(n - 1, m);
    }
}
```

- **PR-10.** What is printed from `fun(19)` as coded below? Explain what the function does.

```cpp
void fun (int n)
{
    if (n > 0)
    {
        fun (n / 2);
        cout << n % 2;
    }
}
```

## Programs

- **PRG-1.** Write a tail version of the *factorial* function and add a nonrecursive function to call it. Test the function in a program.

- **PRG-2.** Write a recursive function to find the number of permutations of *n* objects *k* at a time and then write a program to test it. The formula is given below:
  `P(n, k) = factorial(n) / factorial(n - k)`

- **PRG-3.** Write a recursive function to find the combination of *n* objects *k* at a time. Then write a program to test it. The formula is given below:
  `C(n, k) = factorial(n) / (factorial(n - k) * factorial(k))`

- **PRG-4.** Write a recursive *tail* function that reverses the digits in its argument. For example, given the integer 12789, the function returns 98721. Then use a nonrecursive function to call it. Test the functions in a program.

- **PRG-5.** Write a *tail* recursive function to convert a decimal integer to a binary string and then use a nonrecursive function to call it. For example, the decimal 78 will be changed to “1001110”. Test your functions in a program.

- **PRG-6.** Write a *tail* recursive function to convert a decimal integer to a string of hexadecimal characters and use a nonrecursive function to call it. For example, the decimal 78 will be changed to “4E”. Test your functions in a program.

- **PRG-7.** Write a *tail* recursive function to find the smallest integer in an array of integers. Then use a nonrecursive function to call it. Test your function in a program with at least three arrays of 10 integers. Note that when we look for the smallest element in an array, we must keep track of the smallest element and the next index to check. This means that your helper function must have two extra parameters.

- **PRG-8.** Write a program that finds all the factors of a given number. A factor is a number less than or equal to the given number that divides the number with remainder zero. Note that any number has at least two factors: 1 and itself. Test your function with the factors of a few numbers and tabulate the results in a program. Write a recursive (helper) function that finds the divisor of two numbers. Then use a nonrecursive function to call it.

- **PRG-9.** Write a tail recursive function and the corresponding nonrecursive function to test if an integer is prime. Remember that a prime number is only divisible by 1 and itself, but we can check the numbers from 1 to the square root of that number to be sure that it is prime. Remember that 1 is not a prime. Mathematicians divide the positive integers into three groups: composite, prime, and 1.

- **PRG-10.** Write a program to find all prime factors of a given number. A prime factor is an integer that is a factor and is also a prime. Prime factors have many applications in the field of security and cryptography. In writing your program, feel free to use the ideas presented in PRG-8 and PRG-9.

- **PRG-11.** Write a recursive function that counts and prints the number of a given character in a string. Test the function in a program.
