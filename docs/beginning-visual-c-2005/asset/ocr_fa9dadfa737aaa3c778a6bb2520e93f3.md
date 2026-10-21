# Chapter 3

Naturally, the original declaration for i would need to be omitted in the program. If you make this change to the last example, you will find that it now does not compile because the loop variable, i, ceases to exist after the loop so you cannot refer to it in the output statement. A loop has a scope which extends from the for expression to the end of the body of the loop, which of course can be a block of code between braces, as well as just a single statement. The counter i is now declared within the loop scope, so you cannot refer to it in the output statement because this is outside the scope of the loop. By default the C++ compiler enforces the ISO/ANSI C++ standard by insisting that a variable defined within a loop condition cannot be referenced outside the loop. If you need to use the value in the counter after the loop has executed, you must declare the counter variable outside the scope of the loop.

You can omit the initialization expression altogether from the loop. If you initialize i appropriately in the declaration statement for it, you can write the loop as:

```
```cpp
int i = 1;
for(; i <= max; i++)                 // Loop specification
    sum += i;                         // Loop statement
```
```

You still need the semicolon that separates the initialization expression from the test condition for the loop. In fact, both semicolons must always be present regardless of whether any or all of the control expressions are omitted. If you omit the first semicolon, the compiler is unable to decide which expression has been omitted or even which semicolon is missing.

The loop statement can be empty. For example, you could place the loop statement in for loop from the previous example inside the increment expression; in this case the loop becomes

```
```cpp
for(i = 1; i <= max; sum += i++);       // The whole loop
```
```

You still need the semicolon after the closing parentheses, to indicate that the loop statement is now empty. If you omit this, the statement immediately following this line is interpreted as the loop statement. Sometime you’ll see the empty loop statement written on a separate line like the following.

```
```cpp
for(i = 1; i <= max; sum += i++)         // The whole loop
    ;
```
```

# Try It Out    Using Multiple Counters

You can use the comma operator to include multiple counters in a for loop. You can see this in operation in the following program.

```
```cpp
// Ex3_09.cpp
// Using multiple counters to show powers of 2
#include <iostream>
#include <iomanip>

using std::cin;
using std::cout;
using std::endl;
using std::setw;

int main()
{
```
```