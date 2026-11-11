| `java.nio.file.Path` |
|---|
| • `static Path of(String pathname)` ¹¹<br>constructs a Path from the given path name. |

# 3.8 Control Flow

Java, like any programming language, supports both conditional statements and loops to determine control flow. We will start with the conditional statements, then move on to loops, to end with the somewhat cumbersome switch statement that you can use to test for many values of a single expression.

> > **C++ NOTE:** The Java control flow constructs are identical to those in C and C++, with a few exceptions. There is no goto, but there is a “labeled” version of break that you can use to break out of a nested loop (where, in C, you perhaps would have used a goto). Finally, there is a variant of the for loop that is similar to the range-based for loop in C++ and the foreach loop in C#.

# 3.8.1 Block Scope

Before learning about control structures, you need to know more about blocks.

A block, or compound statement, consists of a number of Java statements, surrounded by a pair of braces. Blocks define the scope of your variables. A block can be nested inside another block. Here is a block that is nested inside the block of the main method:

```
public static void main(String[] args)
{
    int n;
    . . .
    {
        int k;
        . . .
    } // k is only defined up to here
}
```

You may not declare identically named variables in two nested blocks. For example, the following is an error and will not compile:

```
public static void main(String[] args)
{
    int n;
    . . .
```