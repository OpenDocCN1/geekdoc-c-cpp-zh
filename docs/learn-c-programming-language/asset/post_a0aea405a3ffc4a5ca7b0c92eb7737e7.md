
| Category | Operators | Associativity |
|---|---|---|
| Additive | `+ -` | Left to right |
| Shift | `<< >>` | Left to right |
| Relational | `< <= > >=` | Left to right |
| Equality | `== !=` | Left to right |
| Bitwise AND | `&` | Left to right |
| Bitwise XOR | `^` | Left to right |
| Bitwise OR | `|` | Left to right |
| Logical AND | `&&` | Left to right |
| Logical OR | `||` | Left to right |
| Conditional | `?:` | Right to left |
| Assignment | `= += -= *= /= %= >>= <<= &= ^= |=` | Right to left |
| Comma | `,` | Left to right |

Try the following example to understand operator’s precedence concept available in C++. Copy and paste the following C++ program in test.cpp file and compile and run this program.

Check the simple difference with and without parenthesis. This will produce different results because (), /, * and + have different precedence. Higher precedence operators will be evaluated first:

```
```cpp
#include <iostream>

using namespace std;

main()
{
    int a = 20;
```
```

## 12. LOOP TYPES

There may be a situation, when you need to execute a block of code several number of times. In general, statements are executed sequentially: The first statement in a function is executed first, followed by the second, and so on.

Programming languages provide various control structures that allow for more complicated execution paths.

A loop statement allows us to execute a statement or group of statements multiple times and following is the general form of a loop statement in most of the programming languages:

![](img/7976f323fd1a5c8774f95fbf029a106f_62_0.png)

C++ programming language provides the following type of loops to handle looping requirements.

| Loop Type | Description |
|---|---|
| while loop | Repeats a statement or group of statements while a given condition is true. It tests the condition before executing the loop body. |
| for loop | Execute a sequence of statements multiple times and abbreviates the code that manages the loop variable. |

|  |  |
|---|---|
| do...while loop | Like a ‘while’ statement, except that it tests the condition at the end of the loop body. |
| nested loops | You can use one or more loop inside any another ‘while’, ‘for’ or ‘do...while’ loop. |

## While Loop

A **while** loop statement repeatedly executes a target statement as long as a given condition is true.

## Syntax

The syntax of a while loop in C++ is:

```
```cpp
while(condition)
{
    statement(s);
}
```
```

Here, **statement(s)** may be a single statement or a block of statements. The **condition** may be any expression, and true is any non-zero value. The loop iterates while the condition is true.

When the condition becomes false, program control passes to the line immediately following the loop.

## Flow Diagram

C++

![](img/7976f323fd1a5c8774f95fbf029a106f_64_0.png)

Here, key point of the *while* loop is that the loop might not ever run. When the condition is tested and the result is false, the loop body will be skipped and the first statement after the while loop will be executed.

## Example

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    // Local variable declaration:
    int a = 10;

    // while loop execution
    while( a < 20 )
    {
        cout << "value of a: " << a << endl;
        a++;
    }
}
```
```

```
```cpp
return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
value of a: 10

value of a: 11

value of a: 12

value of a: 13

value of a: 14

value of a: 15

value of a: 16

value of a: 17

value of a: 18

value of a: 19
```
```

## for Loop

A **for** loop is a repetition control structure that allows you to efficiently write a loop that needs to execute a specific number of times.

## Syntax

The syntax of a for loop in C++ is:

```
```cpp
for ( init; condition; increment )
{
    statement(s);
}
```
```

Here is the flow of control in a for loop:

+   1. The **init** step is executed first, and only once. This step allows you to declare and initialize any loop control variables. You are not required to put a statement here, as long as a semicolon appears.
+   
+   2. Next, the **condition** is evaluated. If it is true, the body of the loop is executed. If it is false, the body of the loop does not execute and flow of control jumps to the next statement just after the for loop.
+   
+   3. After the body of the for loop executes, the flow of control jumps back up to the **increment** statement. This statement allows you to update any
loop control variables. This statement can be left blank, as long as a semicolon appears after the condition.

+   4. The condition is now evaluated again. If it is true, the loop executes and the process repeats itself (body of loop, then increment step, and then again condition). After the condition becomes false, the for loop terminates.

## Flow Diagram

![](img/7976f323fd1a5c8774f95fbf029a106f_66_0.png)

## Example

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    // for loop execution
    for( int a = 10; a < 20; a = a + 1 )
```
```

```
{
    cout << "value of a: " << a << endl;
}

    return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```
value of a: 10
value of a: 11
value of a: 12
value of a: 13
value of a: 14
value of a: 15
value of a: 16
value of a: 17
value of a: 18
value of a: 19
```

## do...while Loop

Unlike for and while loops, which test the loop condition at the top of the loop, the do...while loop checks its condition at the bottom of the loop.

A do...while loop is similar to a while loop, except that a do...while loop is guaranteed to execute at least one time.

## Syntax

The syntax of a do...while loop in C++ is:

```
do
{
    statement(s);
}while( condition );
```

Notice that the conditional expression appears at the end of the loop, so the statement(s) in the loop execute once before the condition is tested.

If the condition is true, the flow of control jumps back up to do, and the statement(s) in the loop execute again. This process repeats until the given condition becomes false.

## Flow Diagram

![](img/7976f323fd1a5c8774f95fbf029a106f_68_0.png)

## Example

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    // Local variable declaration:
    int a = 10;

    // do loop execution
    do
    {
        cout << "value of a: " << a << endl;
        a = a + 1;
    }while( a < 20 );

    return 0;
}
```
```

```
```cpp
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
value of a: 10

value of a: 11

value of a: 12

value of a: 13

value of a: 14

value of a: 15

value of a: 16

value of a: 17

value of a: 18

value of a: 19
```
```

## nested Loops

A loop can be nested inside of another loop. C++ allows at least 256 levels of nesting.

## Syntax

The syntax for a **nested for loop** statement in C++ is as follows:

```
```cpp
for ( init; condition; increment )
{
    for ( init; condition; increment )
    {
        statement(s);
    }
    statement(s); // you can put more statements.
}
```
```

The syntax for a **nested while loop** statement in C++ is as follows:

```
```cpp
while(condition)
{
    while(condition)
    {
        statement(s);
```
```

```
2 is prime
3 is prime
5 is prime
7 is prime
11 is prime
13 is prime
17 is prime
19 is prime
23 is prime
29 is prime
31 is prime
37 is prime
41 is prime
43 is prime
47 is prime
53 is prime
59 is prime
61 is prime
67 is prime
71 is prime
73 is prime
79 is prime
83 is prime
89 is prime
97 is prime
```

## Loop Control Statements

Loop control statements change execution from its normal sequence. When execution leaves a scope, all automatic objects that were created in that scope are destroyed.

C++ supports the following control statements.

| Control Statement | Description |
|---|---|
| break statement | Terminates the **loop** or **switch** statement and transfers execution to the statement immediately |
