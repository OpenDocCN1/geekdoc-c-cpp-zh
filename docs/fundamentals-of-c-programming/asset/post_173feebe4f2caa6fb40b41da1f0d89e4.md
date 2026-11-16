
done = true; // Only troubleshoots power issues
}
}
}
```

The bulk of the body of the Listing 6.9 (troubleshootloop.cpp) is wrapped by a `while` statement. The Boolean variable `done` is often called a `flag`. You can think of the flag being down when the value is false and raised when it is true. In this case, when the flag is raised, it is a signal that the program should terminate.

Notice the last 11 lines of Listing 6.9 (troubleshootloop.cpp):

```
}
}
}
} else { // The computer has power
std::cout << "Please consult a service technician.\n";
done = true; // Only troubleshoots power issues
}
}
}
```

In the way this code is organized, the matching opening curly brace of a particular closing curly brace can be found by scanning upward in the source code until the closest opening curly brace at the same indentation level is found. Our programming logic is now getting complex enough that the proper placement of curly braces is crucial for human readers to more quickly decipher how the program should work. See Section 4.5 for guidelines on indentation and curly brace placement to improve code readability.

## 6.2 Nested Loops

Just like in `if` statements, `while` bodies can contain arbitrary C++ statements, including other `while` statements. A loop can therefore be nested within another loop. To see how nested loops work, consider a program that prints out a multiplication table. Elementary school students use multiplication tables, or times tables, as they learn the products of integers up to 10 or even 12. Figure 6.3 shows a 10 x 10 multiplication table. We want our multiplication table program to be flexible and allow the user to specify the table's size. We will begin our development work with a simple program and add features as we go. First, we will not worry about printing the table's row and column titles, nor will we print the lines separating the tables from the contents of the table. Initially we will print only the contents of the table. We will see we need a nested loop to print the table's contents, but that still is too much to manage in our first attempt. In our first attempt we will print the rows of the table in a very rudimentary manner. Once we are satisfied that our simple program works we can add more features. Listing 6.10 (timestable-1st-try.cpp) shows our first attempt at a multiplication table.

```
Listing 6.10: timestable-1st-try.cpp

#include <iostream>

int main() {
  int size; // The number of rows and columns in the table
  std::cout << "Please enter the table size: ";
std::cin >> size;
// Print a size x size multiplication table
int row = 1;
while (row <= size) { // Table has 10 rows.
    std::cout << "Row #" << row << " ";
    row++;
}
```

### Figure 6.3 A 10 X 10 multiplication table

| x | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
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

The output of Listing 6.10 (timestable-1st-try.cpp) is somewhat underwhelming:

![](img/e84ad11adb18201d71595b31ce6c9eff_145_0.png)

Listing 6.10 (timestable-1st-try.cpp) does indeed print each row in its proper place—it just does not supply the needed detail for each row. Our next step is to refine the way the program prints each row. Each row should contain size numbers. Each number within each row represents the product of the current row and current column, for example, the number in row 2, column 5 should be 2 x 5 = 10. In each row, therefore, we must vary the column number from 1 to size. Listing 6.11 (timestable-2nd-try.cpp) contains the needed refinement.

```
Listing 6.11: timestable-2nd-try.cpp
#include <iostream>
int main() {
int size; // The number of rows and columns in the table
std::cout << "Please enter the table size: ";
std::cin >> size;
// Print a size x size multiplication table
int row = 1;
while (row <= size) { // Table has size rows.
    int column = 1; // Reset column for each row.
    while (column <= size) { // Table has size columns.
        int product = row*column; // Compute product
        std::cout << product << " "; // Display product
        column++; // Next element
    }
    std::cout << '\n'; // Move cursor to next row
    row++; // Next row
}
```

We use a loop to print the contents of each row. The outer loop controls how many total rows the program prints, and the inner loop, executed in its entirety each time the program prints a row, prints the individual elements that make up a row.

The result of Listing 6.11 (timestable-2nd-try.cpp) is

| Please enter the table size: 10 |
| --- |
| 1 2 3 4 5 6 7 8 9 10 |
| 2 4 6 8 10 12 14 16 18 20 |
| 3 6 9 12 15 18 21 24 27 30 |
| 4 8 12 16 20 24 28 32 36 40 |
| 5 10 15 20 25 30 35 40 45 50 |
| 6 12 18 24 30 36 42 48 54 60 |
| 7 14 21 28 35 42 49 56 63 70 |
| 8 16 24 32 40 48 56 64 72 80 |
| 9 18 27 36 45 54 63 72 81 90 |
| 10 20 30 40 50 60 70 80 90 100 |

The numbers within each column are not lined up nicely, but the numbers are in their correct positions relative to each other. We can use the std::setw stream manipulator introduced in Listing 6.7 (powersof10justified.cpp) to right justify the numbers within a four-digit area. Listing 6.12 (timestable-3rd-try.cpp) contains this alignment adjustment.

### Listing 6.12: timestable-3rd-try.cpp

```
#include <iostream>
#include <iomanip>
int main() {
    int size; // The number of rows and columns in the table
    std::cout << "Please enter the table size: ";
    std::cin >> size;
    // Print a size x size multiplication table
    int row = 1;
    while (row <= size) { // Table has size rows.
        int column = 1; // Reset column for each row.
        while (column <= size) { // Table has size columns.
            int product = row*column; // Compute product
std::cout << std::setw(4) << product; // Display product
column++; // Next element
}
std::cout << '\n'; // Move cursor to next row
row++; // Next row
}
```

Listing 6.12 (timestable-3rd-try.cpp) produces the table's contents in an attractive form:

```
Please enter the table size: 10
1   2   3   4   5   6   7   8   9   10
2   4   6   8   10  12  14  16  18  20
3   6   9   12  15  18  21  24  27  30
4   8   12  16  20  24  28  32  36  40
5   10  15  20  25  30  35  40  45  50
6   12  18  24  30  36  42  48  54  60
7   14  21  28  35  42  49  56  63  70
8   16  24  32  40  48  56  64  72  80
9   18  27  36  45  54  63  72  81  90
10  20  30  40  50  60  70  80  90  100
```

Input values of 5:

```
Please enter the table size: 5
1   2   3   4   5
2   4   6   8   10
3   6   9   12  15
4   8   12  16  20
5   10  15  20  25
```

and 15:

```
Please enter the table size: 15
1   2   3   4   5   6   7   8   9   10  11  12  13  14  15
2   4   6   8   10  12  14  16  18  20  22  24  26  28  30
3   6   9   12  15  18  21  24  27  30  33  36  39  42  45
4   8   12  16  20  24  28  32  36  40  44  48  52  56  60
5   10  15  20  25  30  35  40  45  50  55  60  65  70  75
6   12  18  24  30  36  42  48  54  60  66  72  78  84  90
7   14  21  28  35  42  49  56  63  70  77  84  91  98  105
8   16  24  32  40  48  56  64  72  80  88  96  104 112 120
9   18  27  36  45  54  63  72  81  90  99  108 117 126 135
10  20  30  40  50  60  70  80  90  100 110 120 130 140 150
11  22  33  44  55  66  77  88  99  110 121 132 143 154 165
12  24  36  48  60  72  84  96  108 120 132 144 156 168 180
13  26  39  52  65  78  91  104 117 130 143 156 169 182 195
14  28  42  56  70  84  98  112 126 140 154 168 182 196 210
15  30  45  60  75  90  105 120 135 150 165 180 195 210 225
```

also give good results.

All that is left is to add the row and column titles and the lines that bound the edges of the table. Listing 6.13 (timestable.cpp) adds the necessary code.
