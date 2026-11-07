
Repeat Steps c.2 through c.5 until the Fibonacci number you want is calculated.

The following `while` loop executes Steps c.2 through c.5 and determines the *nth* Fibonacci number.

```cpp
while (counter <= nthFibonacci)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
    counter++;
}
```

- 7. Output the nthFibonacci number, which is stored in the variable current.

## COMPLETE PROGRAM LISTING

```cpp
//******************************************************************
// Author: D. S. Malik
//
// Program: nth Fibonacci number
// Given the first two numbers of a Fibonacci sequence, this
// determines and outputs the desired number of the Fibonacci
// sequence.
//******************************************************************

#include <iostream>

using namespace std;

int main()
{
        //Declare variables
        int previous1;
        int previous2;
        int current;
        int counter;
        int nthFibonacci;

        cout << "Enter the first two Fibonacci "
             << "numbers: ";                         //Step 1
        cin >> previous1 >> previous2;                //Step 2
        cout << endl;

        cout << "The first two Fibonacci numbers are "
             << previous1 << " and " << previous2
             << endl;                                 //Step 3

        cout << "Enter the position of the desired "
             << " Fibonacci number: ";               //Step 4
        cin >> nthFibonacci;                          //Step 5
        cout << endl;

        if (nthFibonacci == 1)
            current = previous1;
        else if (nthFibonacci == 2)
            current = previous2;
        else
        {
            counter = 3;
            while (counter <= nthFibonacci)
            {
                current = previous2 + previous1;
                previous1 = previous2;
                previous2 = current;
                counter++;
            }//end while
        }//end else

        cout << "The Fibonacci number at position "
             << nthFibonacci << " is " << current
             << endl;

        return 0;
}//end main
```

## Sample Runs:

### Sample Run 1:

```text
Enter the first two Fibonacci numbers: 12 16
The first two Fibonacci numbers are 12 and 16
Enter the position of the desired Fibonacci number: 10
The Fibonacci number at position 10 is 796
```

### Sample Run 2:

```text
Enter the first two Fibonacci numbers: 1 1
The first two Fibonacci numbers are 1 and 1
Enter the position of the desired Fibonacci number: 15
The Fibonacci number at position 15 is 610
```

## for Looping (Repetition) Structure

The while loop discussed in the previous section is general enough to implement most forms of repetitions. The C++ for looping structure discussed here is a specialized form of the while loop. Its primary purpose is to simplify the writing of counter-controlled loops. For this reason, the for loop is typically called a counter or indexed for loop.

The general form of the `for` statement is:

```cpp
for (initial statement; loop condition; update statement)
    statement
```

The initial statement, loop condition, and update statement (called `for` loop control statements) enclosed within the parentheses control the body (statement) of the `for` statement. Figure 5-2 shows the flow of execution of a `for` loop.

![](img/b217c421655b51e7494cf3b89bb5432d_347_0.png)

**FIGURE 5-2** `for` loop

The `for` loop executes as follows:

- 1. The `initial statement` executes.
- 2. The `loop condition` is evaluated. If the `loop condition` evaluates to `true`:
  - i. Execute the `for` loop statement.
  - ii. Execute the `update statement` (the third expression in the parentheses).
- 3. Repeat Step 2 until the `loop condition` evaluates to `false`.

The `initial statement` usually initializes a variable (called the `for` loop control, or `for` indexed, variable).

In C++, `for` is a reserved word.

> **NOTE** As the name implies, the initial statement in the `for` loop is the first statement to execute; it executes only once.

### EXAMPLE 5-9

The following `for` loop prints the first 10 nonnegative integers:

```cpp
for (i = 0; i < 10; i++)
    cout << i << " ";
cout << endl;
```

The initial statement, `i = 0;`, initializes the `int` variable `i` to 0. Next, the loop condition, `i < 10`, is evaluated. Because `0 < 10` is true, the print statement executes and outputs 0. The update statement, `i++`, then executes, which sets the value of `i` to 1. Once again, the loop condition is evaluated, which is still true, and so on. When `i` becomes 10, the loop condition evaluates to `false`, the `for` loop terminates, and the first statement following the `for` loop executes.

A `for` loop can have either a simple or compound statement.

The following examples further illustrate how a `for` loop executes.

### EXAMPLE 5-10

- 1. The following `for` loop outputs `Hello!` and a star (on separate lines) five times:
  
  ```cpp
  for (i = 1; i <= 5; i++)
  {
      cout << "Hello!" << endl;
      cout << "*" << endl;
  }
  ```
  
- 2. Consider the following `for` loop:
  
  ```cpp
  for (i = 1; i <= 5; i++)
      cout << "Hello!" << endl;
      cout << "*" << endl;
  ```
  
  The output of this `for` loop is:
  
  ```text
  Hello!
  Hello!
  Hello!
  Hello!
  Hello!
  *
  ```
  
  The `for` loop controls only the first output statement because the two output statements are not made into a compound statement using braces. Therefore, the first output statement executes five times because the `for` loop body executes five times. After the `for` loop executes, the second output statement executes only once. The indentation, which is ignored by the compiler, is nevertheless misleading.

### EXAMPLE 5-12

You can count backward using a `for` loop if the `for` loop control expressions are set correctly.

For example, consider the following `for` loop:

```cpp
for (i = 10; i >= 1; i--)
    cout << " " << i;
cout << endl;
```

The output is:

```text
10  9  8  7  6  5  4  3  2  1
```

In this `for` loop, the variable `i` is initialized to 10. After each iteration of the loop, `i` is decremented by 1. The loop continues to execute as long as `i >= 1`.

### EXAMPLE 5-13

You can increment (or decrement) the loop control variable by any fixed number. In the following `for` loop, the variable `i` is initialized to 1; at the end of the `for` loop, `i` is incremented by 2. This `for` loop outputs the first 10 positive odd integers.

```cpp
for (i = 1; i <= 20; i = i + 2)
    cout << " " << i;
cout << endl;
```

The output is:

```text
1  3  5  7  9  11  13  15  17  19
```

### EXAMPLE 5-14

Suppose that `i` is an `int` variable.

- 1. Consider the following `for` loop:
  
  ```cpp
  for (i = 10; i <= 9; i++)
      cout << i << " ";
  cout << endl;
  ```
  
  In this `for` loop, the initial statement sets `i` to 10. Because initially the loop condition (`i <= 9`) is `false`, nothing happens.
  
- 2. Consider the following `for` loop:
  
  ```cpp
  for (i = 9; i >= 10; i--)
      cout << i << " ";
  cout << endl;
  ```
  
  In this `for` loop, the initial statement sets `i` to 9. Because initially the loop condition (`i >= 10`) is `false`, nothing happens.
  
- 3. Consider the following `for` loop:
  
  ```cpp
  for (i = 10; i <= 10; i++)        //Line 1
      cout << i << " ";             //Line 2
  cout << endl;                     //Line 3
  ```
  
  In this `for` loop, the initial statement sets `i` to 10. The loop condition (`i <= 10`) evaluates to `true`, so the output statement in Line 2 executes, which outputs 10. Next, the update statement increments the value of `i` by 1, so the value of `i` becomes 11. Now the loop condition evaluates to `false` and the `for` loop terminates. Note that the output statement in Line 2 executes only once.
  
- 4. Consider the following `for` loop:
  
  ```cpp
  for (i = 1; i <= 10; i++);        //Line 1
      cout << i << " ";             //Line 2
  cout << endl;                     //Line 3
  ```
  
  This `for` loop has no effect on the output statement in Line 2. The semi-colon at the end of the `for` statement terminates the `for` loop; the action of the `for` loop is thus empty. The output statement is all by itself and executes only once.
  
- 5. Consider the following `for` loop:
  
  ```cpp
  for (i = 1; ; i++)
      cout << i << " ";
  cout << endl;
  ```
  
  In this `for` loop, because the loop condition is omitted from the `for` statement, the loop condition is always `true`. This is an infinite loop.
  
- 6. The following `for` loop outputs the positive powers of 2 up to 100.
  
  ```cpp
  for (i = 2; i < 100; i = 2 * i)
      cout << i << " ";          //output power of 2
  cout << endl;
  ```
  
  The output is:
  
  ```text
  2 4 8 16 32 64
  ```
