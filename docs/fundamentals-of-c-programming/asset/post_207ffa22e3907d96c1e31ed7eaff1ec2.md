
## Listing 6.13: timestable.cpp

```cpp
#include <iostream>
#include <iomanip>

int main() {
    int size; // The number of rows and columns in the table
    std::cout << "Please enter the table size: ";
    std::cin >> size;
    // Print a size x size multiplication table

    // First, print heading: 1 2 3 4 5 etc.
    std::cout << " " << " "; // Print heading
    // Print column heading
    int column = 1;
    while (column <= size) {
        std::cout << std::setw(4) << column; // Print heading for this column.
        column++;
    }

    std::cout << '\n';

    // Print line separator: +-------
    std::cout << " +";
    column = 1;
    while (column <= size) {
        std::cout << "-----"; // Print line for this column.
        column++;
    }

    std::cout << '\n';

    // Print table contents
    int row = 1;
    while (row <= size) { // Table has size rows.
        std::cout << std::setw(2) << row << "|"; // Print heading for row.
        int column = 1; // Reset column for each row.
        while (column <= size) { // Table has size columns.
            int product = row*column; // Compute product
            std::cout << std::setw(4) << product; // Display product
            column++; // Next element
        }
        row++;
        std::cout << '\n'; // Move cursor to next row
    }
}
```

When the user supplies the value 10, Listing 6.13 (timestable.cpp) produces

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 2 | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 |
| 3 | 3 | 6 | 9 | 12 | 15 | 18 | 21 | 24 | 27 | 30 |
| 4 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 |
| 5 | 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 | 45 | 50 |
| 6 | 6 | 12 | 18 | 24 | 30 | 36 | 42 | 48 | 54 | 60 |
| 7 | 7 | 14 | 21 | 28 | 35 | 42 | 49 | 56 | 63 | 70 |
| 8 | 8 | 16 | 24 | 32 | 40 | 48 | 56 | 64 | 72 | 80 |
| 9 | 9 | 18 | 27 | 36 | 45 | 54 | 63 | 72 | 81 | 90 |
| 10 | 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 | 90 | 100 |

An input of 15 yields

```
Please enter the table size: 15
 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15
+---------------------------------------------
1 | 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15
2 | 2  4  6  8 10 12 14 16 18 20 22 24 26 28 30
3 | 3  6  9 12 15 18 21 24 27 30 33 36 39 42 45
4 | 4  8 12 16 20 24 28 32 36 40 44 48 52 56 60
5 | 5 10 15 20 25 30 35 40 45 50 55 60 65 70 75
6 | 6 12 18 24 30 36 42 48 54 60 66 72 78 84 90
7 | 7 14 21 28 35 42 49 56 63 70 77 84 91 98 105
8 | 8 16 24 32 40 48 56 64 72 80 88 96 104 112 120
9 | 9 18 27 36 45 54 63 72 81 90 99 108 117 126 135
10| 10 20 30 40 50 60 70 80 90 100 110 120 130 140 150
11| 11 22 33 44 55 66 77 88 99 110 121 132 143 154 165
12| 12 24 36 48 60 72 84 96 108 120 132 144 156 168 180
13| 13 26 39 52 65 78 91 104 117 130 143 156 169 182 195
14| 14 28 42 56 70 84 98 112 126 140 154 168 182 196 210
15| 15 30 45 60 75 90 105 120 135 150 165 180 195 210 225
```

If the user enters 7, the program prints

```
Please enter the table size: 7
 1  2  3  4  5  6  7
+--------------------
1 | 1  2  3  4  5  6  7
2 | 2  4  6  8 10 12 14
3 | 3  6  9 12 15 18 21
4 | 4  8 12 16 20 24 28
5 | 5 10 15 20 25 30 35
6 | 6 12 18 24 30 36 42
7 | 7 14 21 28 35 42 49
```

The user even can enter a 1:

```
Please enter the table size: 1
 1
+-
1 | 1
```

As we can see, the table automatically adjusts to the size and spacing required by the user's input.

This is how Listing 6.13 (timestable.cpp) works:

- It is important to distinguish what is done only once (outside all loops) from that which is done repeatedly. The column heading across the top of the table is outside all of the loops; therefore, it is printed all at once.
- The work to print the heading for the rows is distributed throughout the execution of the outer loop. This is because the heading for a given row cannot be printed until all the results for the previous row have been printed.
- In the nested loop, row is the control variable for the outer loop; column controls the inner loop.
- The inner loop executes size times on every single iteration of the outer loop. How many times is the statement
  ```cpp
  std::cout << product << " "; // Display product
  ```
  executed? size x size times, one time for every product in the table.
- A newline is printed after the contents of each row is displayed; thus, all the values printed in the inner (column) loop appear on the same line.

Nested loops are used when an iterative process itself must be repeated. In our times table example, a while loop is used to print the contents of each row, but multiple rows must be printed. The inner loop prints the contents of each row, while the outer is responsible for printing all the rows.

Listing 6.14 (permuteabc.cpp) uses a triply-nested loop to print all the different arrangements of the letters A, B, and C. Each string represents a permutation of ABC.

## Listing 6.14: permuteabc.cpp

```cpp
// File permuteabc.cpp
#include <iostream>
int main() {
  char first = 'A'; // The first letter varies from A to C
  while (first <= 'C') {
    char second = 'A'; // The second varies from A to C
    while (second <= 'C') {
      if (second != first) { // No duplicate letters
        char third = 'A'; // The third varies from A to C
        while (third <= 'C') { // Don't duplicate first or second letter
          if (third != first && third != second) {
            std::cout << first << second << third << '\n';
            third++;
          }
        }
        second++;
      }
      first++;
    }
  }
}
```

Notice how the if statements are used to prevent duplicate letters within a given string. The output of Listing 6.14 (permuteabc.cpp) is all six permutations of ABC:

```
ABC
ACB
BAC
BCA
```

## 6.3 Abnormal Loop Termination

By default, a `while` statement executes until its condition becomes false. The executing program checks this condition only at the “top” of the loop. This means that even if the Boolean expression that makes up the condition becomes false before the program completes executing all the statements within the body of the loop, all the remaining statements in the loop’s body must complete before the loop can once again check its condition. In other words, the `while` statement in and of itself cannot exit its loop somewhere in the middle of its body.

Ordinarily this behavior is not a problem. Usually the intention is to execute all the statements within the body as an indivisible unit. Sometimes, however, it is desirable to immediately exit the body or recheck the condition from the middle of the loop instead. C++ provides the `break` and `continue` statements to give programmers more flexibility designing the control logic of loops.

### 6.3.1 The break statement

C++ provides the `break` statement to implement middle-exiting control logic. The `break` statement causes the immediate exit from the body of the loop. Listing 6.15 (`addmiddleexit.cpp`) is a variation of Listing 6.4 (`addnonnegatives.cpp`) that illustrates the use of `break`.

```
Listing 6.15: addmiddleexit.cpp

#include <iostream>

int main() {
    int input, sum = 0;
    std::cout << "Enter numbers to sum, negative number ends list:";
    while (true) {
        std::cin >> input;
        if (input < 0)
            break; // Exit loop immediately
        sum += input;
    }
    std::cout << "Sum = " << sum << '\n';
}
```

The condition of the `while` in Listing 6.15 (`addmiddleexit.cpp`) is a tautology. This means the condition is true and can never be false. When the program’s execution reaches the `while` statement it is guaranteed to enter the loop’s body and the `while` loop itself does not provide a way of escape. The `if` statement in the loop’s body:

```
if (input < 0) // Is input negative
    break; // If so, exit the loop immediately
```

provides the necessary exit. In this case the `break` statement, executed conditionally based on the value of the variable `input`, exits the loop. In Listing 6.15 (`addmiddleexit.cpp`) the `break` statement executes only when the user enters a negative number. When the program’s execution encounters the `break` statement,
