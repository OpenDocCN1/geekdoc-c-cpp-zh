A block consists of an optional statement_list (§12.3.2), enclosed in braces. If the statement list is omitted, the block is said to be empty.

A block may contain declaration statements (§12.6). The scope of a local variable or constant declared in a block is the block.

A block is executed as follows:

+   - If the block is empty, control is transferred to the end point of the block.
+   - If the block is not empty, control is transferred to the statement list. When and if control reaches the end point of the statement list, control is transferred to the end point of the block.

The statement list of a block is reachable if the block itself is reachable.

The end point of a block is reachable if the block is empty or if the end point of the statement list is reachable.

A block that contains one or more yield statements (§12.15) is called an iterator block. Iterator blocks are used to implement function members as iterators (§14.14). Some additional restrictions apply to iterator blocks:

+   - It is a compile-time error for a return statement to appear in an iterator block (but yield return statements are permitted).
+   - It is a compile-time error for an iterator block to contain an unsafe context (§22.2). An iterator block always defines a safe context, even when its declaration is nested in an unsafe context.

# 12.3.2 Statement lists

A statement list consists of one or more statements written in sequence. Statement lists occur in blocks (§12.3) and in switch_blocks (§12.8.3).

```
statement_list
    : statement+
    ;
```

A statement list is executed by transferring control to the first statement. When and if control reaches the end point of a statement, control is transferred to the next statement. When and if control reaches the end point of the last statement, control is transferred to the end point of the statement list.

A statement in a statement list is reachable if at least one of the following is true:

+   - The statement is the first statement and the statement list itself is reachable.
+   - The end point of the preceding statement is reachable.
+   - The statement is a labeled statement and the label is referenced by a reachable goto statement.

The end point of a statement list is reachable if the end point of the last statement in the list is reachable.

# 12.4 The empty statement

An empty_statement does nothing.

```
empty_statement
    : ';'
    ;
```