| Standard algebraic equality or relational operator | C++ equality or relational operator | Sample C++ condition | Meaning of C++ condition |
|---|---|---|---|
| *Relational operators* | | | |
| > | > | x > y | x is greater than y |
| < | < | x < y | x is less than y |
| ≥ | >= | x >= y | x is greater than or equal to y |
| ≤ | <= | x <= y | x is less than or equal to y |
| *Equality operators* | | | |
| = | == | x == y | x is equal to y |
| ≠ | != | x != y | x is not equal to y |

Fig. 2.12 | Equality and relational operators.

![](bbox=[0.171, 0.449, 0.244, 0.494])

# ### Common Programming Error 2.7

> > Confusing the equality operator `==` with the assignment operator `=` results in logic errors. The equality operator should be read “is equal to,” and the assignment operator should be read “gets” or “is assigned the value of.” Some people prefer to read the equality operator as “double equals.” As we discuss in Section 5.9, confusing these operators may not necessarily cause an easy-to-recognize syntax error, but may cause extremely subtle logic errors.

The following example uses six `if` statements to compare two numbers input by the user. If the condition in any of these `if` statements is satisfied, the output statement associated with that `if` statement is executed. Figure 2.13 shows the program and the input/output dialogs of three sample executions.

```
```cpp
1  // Fig. 2.13: fig02_13.cpp
2  // Comparing integers using if statements, relational operators
3  // and equality operators.
4  #include <iostream> // allows program to perform input and output
5
6  using std::cout; // program uses cout
7  using std::cin; // program uses cin
8  using std::endl; // program uses endl
9
10 // function main begins program execution
11 int main()
12 {
13    int number1; // first integer to compare
14    int number2; // second integer to compare
15
16    cout << "Enter two integers to compare: "; // prompt user for data
17    cin >> number1 >> number2; // read two integers from user
```
```

Fig. 2.13 | Comparing integers using if statements, relational operators and equality operators. (Part 1 of 2.)