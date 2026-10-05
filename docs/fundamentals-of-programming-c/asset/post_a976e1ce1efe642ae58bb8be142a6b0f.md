
## 7.3. THE DO/WHILE STATEMENT

(n < 0) ? -n : n

Some argue the conditional operator is cryptic, and thus reduces a program's readability. seasoned C++ programmers consider it quite understandable, but it is used sparingly because of its very specific nature.

## 7.3 The do/while Statement

An executing program checks the condition of a while statement before executing any of the statements in its body; thus, we say a while loop is a top-checking loop. Sometimes this sequence of checking then executing is inconvenient; for example,

The while statement (Section 6.1) checks its condition before its body is executed; then, it is a top-checking loop. This sequence of checking the condition first executing the body is inconvenient; for example, Listing 7.2 (goodinputoutput.cpp).

```
Listing 7.2: goodinputoutput.cpp
#include <iostream>
using namespace std;
int main() {
    int value = -1;
    cout << "Please enter an integer in the range 0-10: ";
    // Insist on values in the range 0..10
    while (value < 0 || value > 10) {
        cin >> value;
        // value at this point is guaranteed to be within range
        cout << "Legal value entered was " << value << endl;
    }
}
```

The loop in Listing 7.2 (goodinputoutput.cpp) traps the value in the while until the user provides a number in the desired range. Here's how it works:

- The condition of the while specifies a set that includes all values that are not in the desired range. The initialization of in_value to -1 ensures the condition of the while will be true initially, and thus, the program always execute the loop's body at least once.
- The user does not get a chance to enter a value until execution is inside the loop.
- The only way to escape the loop is through a value that violates the condition—precisely a value in the desired range.

The initialization of in_value before the loop check is somewhat arbitrary. There is only to ensure entry into the loop's body. It seems unnatural for a valid value the user gets to enter it. A loop that checks its condition after its body is executed at least once would be more appropriate. The do/while statement is a bottom-checking loop that behaves exactly in this manner. Listing 7.3 (betterinputoutput.cpp) uses a do/while statement to check for valid input.

```
Listing 7.3: betterinputoutput.cpp
```
#include <iostream>

using namespace std;
int main() {
    int in_value;
    cout << "Please enter an integer in the range 0-10: ";
    // Insist on values in the range 0...10
    do
        cin >> in_value;
    while (in_value < 0 || in_value > 10);
    // at this point is is guaranteed to be within range
    cout << "Legal value entered was " << in_value << endl;
}
```

Notice that there is no need to initialize in_value since it is not used until after it is assigned through the input stream cin. Figure 7.1 compares the flowcharts of a while and do/while loop.

![](img/e326304bd50fbc4f7d5a64c1487eb635_164_0.png)

Figure 7.1: The flowcharts for while and do/while loops

The do/while statement has the general form:

```cpp
do
    statement;
while ( condition );
```

- The reserved words do and while identify a do/while statement. The do and while keywords delimit the loop's body, curly braces are still required if the body consists of more than one statement.
- The condition is associated with the while at the end of the loop. The condition is a Boolean expression and must be enclosed within parentheses.
- The statement is exactly like the statement in the general form of the while loop (Section 6.1). It can be a compound statement enclosed within curly braces.

The body of a do/while statement, while the statement, is guaranteed to execute at least once.
The while loop is a convenience to the programmer and is not an essential programming construct. It is easy to transform any code that uses a do/while statement into code that behaves identically to uses a while statement. In practice, programmers use loops more frequently than do/while loops because more algorithms require top-checking loops than bottom-checking loops. The do/while statement is however for a reason, included in C++. Transforming an algorithm that can be expressed more naturally with a bottom-checking loop one uses a top-checking loop can lead to awkward code. Use do/while when appropriate.

## 7.4 The For Statement

Listing 6.2 (iterativecountoff.cpp). It simply counts from one to five. Counting is a frequent activity performed by computer programs. Certain program elements are required in any program to count:

- A variable must be used to keep track of the count; in Listing 6.2 (iterativecountoff.cpp), count is the aptly named counter variable.
- The counter variable must be given an initial value. In the case of Listing 6.2 (iterativecountoff.cpp), the initial value is 1.
- The variable must be modified (incrementally increased) as the program counts. The modification count++ in 6.2 (iterativecountoff.cpp). A way may be provided to determine if the counting has complete.

## 7.4. THE STATEMENT

C++ provides a specialized loop that packages these four elements into one statement. Called the for statement, its general form is

![](img/e326304bd50fbc4f7d5a64c1487eb635_166_0.png)

- The reserved word for identifies a for statement.
- The loop is controlled by a special variable called the loop variable.
- The Header, contained in parentheses, contains three parts, separated by semicolons;
- Initialization. The initialization part assigns an initial value to the loop variable. If it is declared here, its scope is limited to the loop. This means you are free to use that variable outside the loop. The initialization part is performed one time.
- Condition. The condition part generally changes the loop variable, just like the condition of a while statement. The condition is checked each time before the body is executed.
- Modification. The modification part should be such that the loop will terminate. The modification is performed during each iteration after the body is executed. The statement is like that of any other loop. It may be a compound statement within curly braces.

Any for loop can be rewritten as a while loop. The general form of the for loop given above can be written equivalently as

```cpp
for (initialization; condition; modification) {
    statement;
}
```

Listing 7.4 (forcounttoff.cpp) uses a for statement to count to five.

```
Listing 7.4: forcounttoff.cpp
#include <iostream>
using namespace std;
int main() {
    for (int count = 1; count <= 5; count++)
    cout << count << endl; // Display counter
}
```

With a while loop, the four counting variables (variable declaration, initialization, condition, and modification) can be scattered throughout the code. With a for loop, a programmer should be able to determine all the important information about the loop's control by looking at one statement. Listing 6.12 (timetable.cpp) prints a multiplication table on the screen. We can organize its code by converting all the while statements to for statements. The result use less code, as shown in Listing 7.5 (bettertimetable.cpp).

```
Listing 7.5: bettertimetable.cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    int size; // The number of rows and columns in the table
    cout << "Please enter the table size: ";
    cin >> size;
    // Print a size x size multiplication table
    // First, print heading
    cout << "";
    for (int column = 1; column <= size; column++)
```
