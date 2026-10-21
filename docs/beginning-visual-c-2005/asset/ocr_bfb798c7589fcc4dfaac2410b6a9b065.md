# Unconditional Branching

The if statement provides you with the flexibility to choose to execute one set of statements or another, depending on a specified condition, so the statement execution sequence is varied depending on the values of the data in the program. The goto statement, in contrast, is a blunt instrument. It enables you to branch to a specified program statement unconditionally. The statement to be branched to must be identified by a statement label which is an identifier defined according to the same rules as a variable name. This is followed by a colon and placed before the statement requiring labeling. Here is an example of a labeled statement.

```
myLabel: cout << "myLabel branch has been activated" << endl;
```

This statement has the label myLabel, and an unconditional branch to this statement would be written as follows:

```
goto myLabel;
```

Whenever possible, you should avoid using gotos in your program. They tend to encourage convoluted code that can be extremely difficult to follow.

> Because the goto is theoretically unnecessary in a program — there’s always an alternative approach to using goto — a significant cadre of programmers say you should never use it. I don’t subscribe to such an extreme view. It is a legal statement after all, and there are occasions when it can be convenient. I do, however, recommend that you only use it where you can see an obvious advantage over other options that are available; otherwise, you may end up with convoluted error-prone code that is hard to understand and even harder to maintain.

# Repeating a Block of Statements

The capability to repeat a group of statements is fundamental to most applications. Without this capability, an organization would need to modify the payroll program every time an extra employee was hired, and you would need to reload Halo 2 every time you wanted to play another game. So let’s first understand how a loop works.

# What Is a Loop?

A loop executes a sequence of statements until a particular condition is true (or false). You can actually write a loop with the C++ statements that you have met so far. You just need an if and the dreaded goto. Look at the following example.

```
// Ex3_07.cpp
// Creating a loop with an if and a goto
#include <iostream>

using std::cin;
using std::cout;
using std::endl;

int main()
```