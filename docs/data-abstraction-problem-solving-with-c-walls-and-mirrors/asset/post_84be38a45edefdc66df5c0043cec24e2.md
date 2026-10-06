
# 302 CHAPTER 10 Algorithm Efficiency

## EXERCISES

- 1. Using Big O notation, indicate the time requirement of each of the following tasks in the worst case. Describe any assumptions that you make.
    - a. After arriving at a party, you shake hands with each person there.
    - b. Each person in a room shakes hands with everyone else in the room.
    - c. You climb a flight of stairs.
    - d. You slide the banister.
    - e. After entering an elevator, you press a button to choose a floor.
    - f. You ride the elevator from the ground up to the nth floor.
    - g. You read a book twice.
- 2. Describe a way to climb from the bottom of a flight of stairs to the top in time that is no better than O(n²).
- 3. Using Big O notation, indicate the time requirement of each of the following tasks in the worst case.
    - a. Computing the sum of the first n integers by using a for loop
    - b. Displaying n integers in an array
    - c. Displaying n integers in a sorted linked chain
    - d. Displaying n names in an array of linked chains
    - e. Displaying one array element
    - f. Displaying the last integer in a linked chain
    - g. Searching any n items for a particular value by using a sequential search
    - h. Searching any of n items for a particular value using a binary search
    - i. Adding an item to a stack or o/n items
    - j. Adding an item to a bag of o/n items
- 4. Suppose that your implementation of a particular algorithm appears in C++ as:
```cpp
for (int pass = 1; pass <= n; pass++) {
    for (int index = 0; index < n; index++) {
        for (int count = 1; count < 10; count++) {
            // end for
        }
    } // end for
} // end for
```
The previous code shows only the repetition in the algorithm, not the computations that occur within the loops. These computations are independent of n. What is the Big O of the algorithm? Justify your answer.
- 5. Consider the following C++ function f, which calls the function swap. Assume that swap exists and simply swaps the contents of its arguments. Do not be concerned with f's purpose.
```cpp
void f(int theArray[], int n) {
    for (int j = 0; j < n; ++j) {
        int i = 0;
        while (i <= j) {
            if (theArray[i] < theArray[j]) {
                swap(theArray[i], theArray[j]);
                i++;
            } // end while
        } // end for
    } // end f
```
How many comparisons does f perform? in the worst case,, is a sequential search faster than a binary search? Explain.
- For large arrays, show that any polynomial $f(x) = c_nx^n + c_{n-1}x^{n-1} + \dots + c_1x + c_0$ is $O(x^n)$.
- Show that for all $a, b > 1$, $f(n)$ is $O(n \log n)$ if and only if $f(n)$ is $O(\log n)$. Thus, you can omit the base when writing $O(n)$. Hint: Use the identity $\log n = \log_a n / \log_a b$ for all constants $a, b > 1$.
- Show that $7n^2 + 5n$ is not $O(n)$.
- Consider an array of length $n$ containing positive and negative integers in order. Write C++ code that rearranges the integers so the negative integers appear before the positive ones. Your solution should use
    - a. $O(n^2)$ operations
    - b. $O(n)$ operations

## PROGRAMMING PROBLEMS

For the following programming problems, you need to time a section of code in C++. For example, the following statements state the execution of the function doSomething:
```cpp
#include <ctime>
clock_t start = clock();
doSomething();
clock_t finish = clock();
double all1Time = static_cast<double>(finish - start) / CLOCKS_PER_SEC;
```

Consider the following two:

```cpp
// Loop A
for (i = 1; i <= n; i++)
    for (j = 1; j <= 10000; j++)
        sum = sum + j;
```

```cpp
// Loop B
for (i = 1; i <= n; i++)
    for (j = 1; j <= n; j++)
    sum = sum + j;
```

What is the Big O of each loop? Design and implement an experiment to find a value of $n$ for which Loop B is faster than Loop A.

```cpp
// Loop B
for (i = 1; i <= n; i++)
    for (j = 1; j <= n; j++)
    for (k = 1; k <= n; k++)
        sum = sum + k;
```

## CHAPTER 10 Algorithm Efficiency

- 3. Write a C++ program that implements the three algorithms and times for various values of $n$. The program should display a table of the run times of each algorithm for various values of $n$.

| Algorithm A | Algorithm B | Algorithm C |
| :--- | :--- | :--- |
| sum = 0 | sum = 0 | sum = n * (n + 1) / 2 |
| for i = 1 to n | for i = 1 to n | for i = 1 to n |
| sum = sum + i | for j = 1 to i | sum = sum + i |
| | sum = sum + 1 | |

*(Note: The table structure reconstructed from OCR flow)*

For each of the problems, you will need an implementation of the ADT bag which remove a random entry instead of a specific one.

- 4. Suppose that you have several numbered billiard balls on a pool. At each step you remove a billiard ball from the pool. If the ball is removed $n$, you replace it with $n$ balls whose number is $n/2$, where the division is truncated to an integer. If you remove 52 balls. Using Big O notation, predict the time requirement for this algorithm when initially the pool table contains only the $n$ ball.

Write a program that simulates this. Use a bag of positive integers to represent the balls on the pool table. The time actual execution of the program for various values of $n$ and its performance as a function of $n$. Compare your results with your predicted time requirements.

- 5. Repeat the process, but instead replace the $n$ with balls numbered less than $n$.

- 6. In mythology, the Hydra is a monster with many heads. Every time the hero chopped off a head, two smaller heads would grow in its place. Fortunately for the hero, if the head was small enough, he could chop it off with two more growing in its place. To kill the Hydra, all our hero needed to chop off all the heads.

Write a program that simulates the Hydra. Instead, we will use strings. A bag of strings, represents the Hydra. Every time you remove a string from the bag, delete the first letter of the string and put two copies of the remaining string back into the bag. For example, if you remove HYDRA, you add two copies of YDRA to the bag. If you remove a one-letter word, you add nothing to the bag. To begin, read one word from the keyboard and place it into an empty bag. The Hydra dies when the bag becomes empty.

Using Big O notation, predict the time requirement for this algorithm in terms of the $n$ characters of the initial string. Then the time actual execution of the program for various values of $n$ and its performance as a function of $n$.
