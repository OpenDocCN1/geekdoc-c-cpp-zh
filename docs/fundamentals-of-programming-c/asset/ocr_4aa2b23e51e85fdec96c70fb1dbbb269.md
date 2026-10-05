# 6.2. NESTED LOOPS

```
}
}
```

The bulk of the body of the Listing 6.8 (troubleshootloop.cpp) is wrapped by a while statement. The Boolean value done is often called a flag. You can think of the flag being down when the value is false and raised when it is true. In this case, when the flag is raised, it is a signal that the program should terminate.

Notice the last 11 lines of Listing 6.8 (troubleshootloop.cpp):

```
}
}
else { // The computer has base power
cout << "Please consult a service technician." << endl;
done = true; // Only troubleshoot power issues
}
```

In this way code is organized, the matching opening brace of a particular curly brace can be found by scanning upward in the source code until the closest opening brace at the same indentation is found. Our programming logic is now getting complex enough that the proper placement of curly brace is crucial for human readers to quickly decipher how the program should work. See Section 4.5 for guidelines on indentation and brace placement to improve code readability.

# 6.2 Nested Loops

Just like if statements, while bodies can contain arbitrary C++ statements, including other while statements. A loop can be nested within another loop. To see how nested loops work, consider a program that produces a multiplication table. Elementary students use multiplication tables, or times, as learn the products of integers up to 10 or 12. Figure 6.5 shows a 10 x 10 multiplication table. We want our multiplication table to be flexible and allow the user to specify the table's size. We will begin our development with a simple program and add features as we go. First, we will not worry about printing the table's row and column titles, we will print the lines separating the titles from the contents of the table. Initially we will only print the contents of the table. We will need a nested loop to print the table's contents, but that is still too much to manage in our first attempt. In our first attempt we will print the rows in a very rudimentary manner. We are satisfied that our simple program can add more features. Listing 6.9 (timestep-1st-try.cpp) shows our first attempt at a multiplication table.

Listing 6.9: timetable-1st-try.cpp

```
#include <iostream>

using namespace std;

int main() {
  int size; // The number of rows and columns in the table
```