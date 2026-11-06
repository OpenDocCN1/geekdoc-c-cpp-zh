
File processing is the subject of Chapter 8. Section 8.1 can be covered sooner for an introduction to reading and writing text files. The remainder of the chapter gives additional material for practical applications.

Chapters 9 and 10 introduce the object-oriented features of C++. Chapter 9 introduces class design and implementation. Chapter 10 covers inheritance and polymorphism.

⊕ Four additional chapters are available on the Web. They can be used individually for a capstone chapter, or they can be combined for teaching a two-semester course. (They can also be incorporated into a custom print version of the text; ask your Wiley sales representative for details.)

- Chapter 11. Recursion
- Chapter 12. Sorting and Searching
- Chapter 13. Lists, Stacks, and Queues
- Chapter 14. Sets, Maps, and Priority Queues

Figure 1 shows the dependencies between the chapters.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_8_0.png)

**Figure 1**  
Chapter Dependencies

## A Walkthrough of the Learning Aids

The pedagogical elements in this book work together to focus on and reinforce key concepts and fundamental principles of programming, with additional tips and detail organized to support and deepen these fundamentals. In addition to traditional features, such as chapter objectives and a wealth of exercises, each chapter contains elements geared to today’s visual learner.

Throughout each chapter, **margin notes** show where new concepts are introduced and provide an outline of key ideas.

Annotated **syntax boxes** provide a quick, visual overview of new language constructs.

**Annotations** explain required components and point to more information on common errors or best practices associated with the syntax.

## 4.3 The `for` Loop

The for loop is used when a sequence of statements is to be executed a given number of times. You can use a while loop that is controlled by a counter, as in the following example.

```python
counter = 0
while (counter < 10):
    # Check the counter
    count = count + 1
    counter += 1
```

Because this loop type is so common, there is a special form for it, called the for loop.

```python
for counter in range(10):
    count = count + 1
```

Some people call this loop counter-controlled. In contrast, the while loop is called condition-controlled. You can define each loop in terms of the other.

### Syntax 4.2 — `for` Statement

![](img/5e58fb4c840712efd6ed6fa82bb97f57_9_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_9_1.png)

Analogies to everyday objects are used to explain the nature and behavior of concepts such as variables, data types, loops, and more.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_9_2.png)

### Figure 3 — Execution of a `for` Loop

```cpp
// Initialize counter
counter = 1;

for (counter = 1; counter <= 10; counter++) {
    cout << counter << endl;
}

// Check condition
counter <= 10

// Execute loop body
cout << counter << endl;

// Increment counter
counter = counter + 1;

// Check condition again
counter <= 10
```

> **Progressive figures** trace code segments to help students visualize the program flow. Color is used consistently to make variables and other elements easily recognizable.

```cpp
// Function call
double result1 = cube_value(2);
result1 = 8;
slide_length = 2;

// Initializing function parameter variable
double result1 = cube_value();
double result1 = cube_value();
slide_length = 2;

// About to return the value
double volume = slide_length * slide_length * slide_length;
return volume;
slide_length = 2;
volume = 8;

// After function call
double result1 = cube_value(2);
result1 = 8;
```

### Figure 3 — Parameter Passing

- The parameter variable `slide_length` of the `cube_value` function is created.
- The parameter variable is initialized with the value of the argument that was passed in the call. In our case, `slide_length` is set to 2.
- The function is then called and the value is returned.
- The variable receives the returned value.

> **Self-check exercises** at the end of each section are designed to make students think through the new material—and can spark discussion in lecture.

### SELF-CHECK

12. Write the `for` loop of the `infinite.cpp` program as a `while` loop.

13. How many numbers does this loop print?

```cpp
for (int i = 10; i >= 0; i--) {
    cout << i << endl;
}
```

14. Write a `for` loop that prints all even numbers between 10 and 20 (inclusive).

15. Write a `for` loop that computes the sum of the integers from 1 to n.

16. How would you modify the `for` loop of the `while` loop program to print all values until the investment has doubled?

**Practice it**  Now you can try these exercises at the end of the chapter: R4.2, R4.7, P4.12.

> **Optional engineering exercises** engage students with applications from technical fields.

**Engineering P7.20**  Write a program that simulates the control software for a “people mover” system, a set of driverless trains that move in two concentric circular tracks. A set of switches allows trains to switch tracks.

In your program, the outer and inner tracks should each be divided into ten segments. Each track segment can contain a train at a time. A train moves to an adjacent segment. If that segment is occupied, the adjacent segment in the other track is tried.

Define a Segment structure. Each segment has a pointer to the next and previous segments in its track. A train can be removed from a track when it is occupied, to make room for an adjacent segment in the other track.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_11_0.png)

### `ch05/cube.cpp`

```cpp
#include <iostream>
using namespace std;

// Computes the volume of a cube.
// @param side_length the side length of the cube
// @return the volume

double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}

int main()
{
    double result1 = cube_volume(2);
    double result2 = cube_volume(10);
    cout << "A cube with side length 2 has volume " << result1 << endl;
    cout << "A cube with side length 10 has volume " << result2 << endl;
    return 0;
}
```

### Program Run

```text
A cube with side length 2 has volume 8
A cube with side length 10 has volume 1000
```

> **Program listings** are carefully designed for easy reading, going well beyond simple color coding. Functions are set off by a subtle outline.

**Common Errors** describe the kinds of errors that students often make, with an explanation of why the errors occur, and what to do about them.

## Common Error 2.1 — Using Undefined Variables

You must define a variable before you use it for the first time. For example, the following sequence of statements would not be legal. In your program, the statements are compiled in order. When the compiler reaches the first statement, it does not know that `total_per_guest` will be defined in the next line, and it reports an error.

```cpp
double tax_rate = 1.1;
double total_per_guest = 0.20;
...
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_12_0.png)

**Programming Tips** explain good programming practices, and encourage students to be more productive with tips and techniques such as hand-tracing.

## Programming Tip 3.6 — Hand-Tracing

A very useful technique for understanding whether a program works correctly is called hand-tracing. You simulate the program's activity on a sheet of paper. You can use this method with pseudocode or C++ code. Get an index card, a cocktail napkin, or whatever sheet of paper is within reach. Make a column for each variable. Have the program code handy. Make a row, such as a paper clip, to mark the current statement as you trace through the program. Every time a variable changes, write the new value in the variable table along with the code that caused the change.

For example, let's trace the following program with data from the preceding example. As you can see, the values of `tax1` and `tax2` are different because the values are calculated in a different order.

```cpp
int tax1;
int tax2;
double total = 100.0;
tax1 = ...;
tax2 = ...;
```

| statement | tax1 | tax2 | total |
|---|---:|---:|---:|
| ... | ... | ... | ... |

In lines 18 and 22, `income` and `marital_status` are initialized by input statements.

```cpp
cin >> income;
cin >> marital_status;
```

| statement | tax1 | tax2 | income | marital status |
|---|---:|---:|---:|---|
| ... | ... | ... | ... | ... |

Because `marital_status` is not `5`, we move to the else branch of the outer if statement.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_12_1.png)

Hand-tracing helps you understand whether a program works correctly.

**Special Topics** present optional topics and provide additional explanation of others.

## Special Topic 6.2 — A Sorting Algorithm

A sorting algorithm rearranges the elements of a sequence so that they are stored in sorted order. Here is a simple sorting algorithm, called selection sort. Consider sorting the following array values:

```text
[10] [2] [6] [4] [9]
[2] [10] [6] [4] [9]
```

An obvious first step is to find the smallest element. In this case the smallest element is 2, stored in `values[1]`. You should move the 2 to the beginning of the array. Of course, there is already an element stored in `values[0]`, so this element is moved to where the smallest value was stored.

```text
[2] [10] [6] [4] [9]
[2] [4] [6] [10] [9]
```

Now the first element is in the correct place. In the foregoing figure, the darker color indicates the portion of the array that is already sorted. Next take the minimum of the remaining entries `values[1]`...`values[4]`. That minimum value, 6, is already in the correct place. You don't need to do anything in this case, simply extend the sorted array by one to the right.

```text
[2] [4] [6] [10] [9]
[2] [4] [6] [9] [10]
```

Repeat the process. The minimum value of the unsorted region is 9, which needs to be swapped with the first value of the unsorted region.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_12_2.png)

## Random Fact 4.1 — The First Bug

**Random Facts** provide historical and social information on computing—for interest and to fulfill the “historical and social context” requirements of the ACM/IEEE curriculum guidelines.

According to legend, the first bug was found in the Mark II, a huge electromechanical computer at Harvard University. It really was caused by a bug—a moth was trapped in a relay switch. Actually, from the note that the operator left in the log book next to the moth, it appears as if the moth was found already in the machine at the time.

The pioneering computer scientist Maurice Wilkes wrote, “Somehow, in the Machine Room I remembered to think ahead about possible causes of trouble and that was what eventually saved us.”

Years later, a similar incident occurred when a moth was found inside a computer. This is the origin of the term “debugging.”

![](img/5e58fb4c840712efd6ed6fa82bb97f57_12_3.png)
