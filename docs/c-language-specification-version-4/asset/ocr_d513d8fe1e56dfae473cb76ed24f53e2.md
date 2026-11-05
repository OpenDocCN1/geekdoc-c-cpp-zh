The end point of a statement list is reachable if the end point of the last statement in the list is reachable.

# 8.3 The empty statement

An empty-statement does nothing.

```
empty-statement:
;
```

An empty statement is used when there are no operations to perform in a context where a statement is required.

Execution of an empty statement simply transfers control to the end point of the statement. Thus, the end point of an empty statement is reachable if the empty statement is reachable.

An empty statement can be used when writing a while statement with a null body:

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
    ;
}
```

Also, an empty statement can be used to declare a label just before the closing "}" of a block:

```
void F() {
    ...
    if (done) goto exit;
    ...
}
exit: ;
```

# 8.4 Labeled statements

A labeled-statement permits a statement to be prefixed by a label. Labeled statements are permitted in blocks, but are not permitted as embedded statements.

```
labeled-statement:
    identifier : statement
```

A labeled statement declares a label with the name given by the identifier. The scope of a label is the whole block in which the label is declared, including any nested blocks. It is a compile-time error for two labels with the same name to have overlapping scopes.

A label can be referenced from goto statements (§8.9.3) within the scope of the label. This means that goto statements can transfer control within blocks and out of blocks, but never into blocks.

Labels have their own declaration space and do not interfere with other identifiers. The example

```
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```

is valid and uses the name x as both a parameter and a label.

Execution of a labeled statement corresponds exactly to execution of the statement following the label.

In addition to the reachability provided by normal flow of control, a labeled statement is reachable if the label is referenced by a reachable goto statement. (Exception: If a goto statement is inside a try that includes a finally block, and the labeled statement is outside the try, and the end point of the finally block is unreachable, then the labeled statement is not reachable from that goto statement.)