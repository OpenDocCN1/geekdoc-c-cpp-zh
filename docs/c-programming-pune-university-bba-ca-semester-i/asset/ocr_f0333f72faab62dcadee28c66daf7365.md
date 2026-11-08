**A revised form for a switch statement is as follows:**

```
```
switch (int expression)
{
case label - 1:
    stmt-list-1;
    break;
case label - 2:
    stmt-list-2;
    break;
case label - 3:
    stmt-list-3;
    break;
.
.
.
case label - n:
    stmt-list-n;
    break;
default:
    stmt-list;
}
```
```

During execution, the expression is evaluated. If the value of the expression matches label - 1, then stmt-list-1 will be executed. If not, execution will move on to check label - 2 and so on. If no labels match the expression, default will be executed. Inside each case and at the end of every statement list (except default) there must be a break statement, which terminates the innermost enclosing switch or loop statement.

Here are some final notes about switch statements: the expression being tested must result in an integral value (int or single char), case labels must be integral constants (either literals or named constants), each label within a switch should be unique, and each stmt-list may contain 0 or more statements which do not need to enclosed with curly braces { }.