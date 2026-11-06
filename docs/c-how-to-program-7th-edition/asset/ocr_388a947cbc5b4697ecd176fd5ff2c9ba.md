effect, executable statements. In C++, it's more precise to call a declaration that also reserves memory a definition. Because definitions are declarations, too, we'll use the term “declaration” except when the distinction is important.

```
```cpp
1  // Fig. 5.1: fig05_01.cpp
2  // Counter-controlled repetition.
3  #include <iostream>
4  using namespace std;
5
6  int main()
7  {
8      int counter = 1; // declare and initialize control variable
9
10     while ( counter <= 10 ) // loop-continuation condition
11     {
12         cout << counter << "  ";
13         counter++; // increment control variable by 1
14     } // end while
15
16     cout << endl; // output a newline
17 } // end main
```
```

```
```
1 2 3 4 5 6 7 8 9 10
```
```

**Fig. 5.1** | Counter-controlled repetition.

The declaration and initialization of counter (line 8) also could have been accomplished with the statements

```
```cpp
int counter; // declare control variable
counter = 1; // initialize control variable to 1
```
```

We use both methods of initializing variables.

Line 13 *increments* the loop counter by 1 each time the loop's body is performed. The loop-continuation condition (line 10) in the while statement determines whether the value of the control variable is less than or equal to 10 (the final value for which the condition is true). The body of this while executes even when the control variable is 10. The loop terminates when the control variable is greater than 10 (i.e., when counter is 11).

Figure 5.1 can be made more concise by initializing counter to 0 and by replacing the while statement with

```
```cpp
while ( ++counter <= 10 ) // loop-continuation condition
    cout << counter << "  ";
```
```

This code saves a statement, because the incrementing is done in the while condition before the condition is tested. Also, the code eliminates the braces around the body of the while, because the while now contains only one statement. Coding in such a condensed fashion can lead to programs that are more difficult to read, debug and maintain.

**Common Programming Error 5.1**
*Floating-point values are approximate, so controlling counting loops with floating-point variables can result in imprecise counter values and inaccurate tests for termination.*