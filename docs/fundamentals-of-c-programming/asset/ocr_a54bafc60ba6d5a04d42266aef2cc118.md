```
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

# 6.2 Nested Loops

Just like in `if` statements, `while` bodies can contain arbitrary C++ statements, including other `while` statements. A loop can therefore be nested within another loop. To see how nested loops work, consider a program that prints out a multiplication table. Elementary school students use multiplication tables, or times tables, as they learn the products of integers up to 10 or even 12. Figure 6.3 shows a 10 x 10 multiplication table. We want our multiplication table program to be flexible and allow the user to specify the table's size. We will begin our development work with a simple program and add features as we go. First, we will not worry about printing the table's row and column titles, nor will we print the lines separating the tables from the contents of the table. Initially we will print only the contents of the table. We will see we need a nested loop to print the table's contents, but that still is too much to manage in our first attempt. In our first attempt we will print the rows of the table in a very rudimentary manner. Once we are satisfied that our simple program works we can add more features. Listing 6.10 (timestable-1st-try.cpp) shows our first attempt at a multiplication table.

```
Listing 6.10: timestable-1st-try.cpp

#include <iostream>

int main() {
  int size; // The number of rows and columns in the table
  std::cout << "Please enter the table size: ";
```