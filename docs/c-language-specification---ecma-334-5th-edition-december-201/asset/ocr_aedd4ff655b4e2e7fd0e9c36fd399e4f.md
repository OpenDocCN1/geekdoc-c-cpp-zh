# 13. Statements

# 13.1 General

C# provides a variety of statements. [Note: Most of these statements will be familiar to developers who have programmed in C and C++. end note]

+   statement:
+   - labeled-statement
+   - declaration-statement
+   - embedded-statement
+   
+   embedded-statement:
+   - block
+   - empty-statement
+   - expression-statement
+   - selection-statement
+   - iteration-statement
+   - jump-statement
+   - try-statement
+   - checked-statement
+   - unchecked-statement
+   - lock-statement
+   - using-statement
+   - yield-statement

The embedded-statement nonterminal is used for statements that appear within other statements. The use of embedded-statement rather than statement excludes the use of declaration statements and labeled statements in these contexts. [Example: The code

```
void F(bool b) {
    if (b)
        int i = 44;
}
```

results in a compile-time error because an if statement requires an embedded-statement rather than a statement for its if branch. If this code were permitted, then the variable i would be declared, but it could never be used. Note, however, that by placing i’s declaration in a block, the example is valid. end example]

# 13.2 End points and reachability

Every statement has an end point. In intuitive terms, the end point of a statement is the location that immediately follows the statement. The execution rules for composite statements (statements that contain embedded statements) specify the action that is taken when control reaches the end point of an embedded statement. [Example: When control reaches the end point of a statement in a block, control is transferred to the next statement in the block. end example]

If a statement can possibly be reached by execution, the statement is said to be reachable. Conversely, if there is no possibility that a statement will be executed, the statement is said to be unreachable.

[Example: In the following code