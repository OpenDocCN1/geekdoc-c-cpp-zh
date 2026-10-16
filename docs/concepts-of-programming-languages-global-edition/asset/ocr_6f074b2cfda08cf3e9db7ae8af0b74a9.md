The semantics of this case expression is that the Boolean expressions are evaluated one at a time, top to bottom. The value of the case expression is the value of the first then expression whose Boolean expression is true. The else represents true in this statement, and the else clause is optional. For example,³

```
leap = case
  when year % 400 == 0 then true
  when year % 100 == 0 then false
  else year % 4 == 0
end
```

This case expression evaluates to true if year is a leap year.

The other Ruby case expression form is similar to the switch of Java. Perl, Python, and Lua do not have multiple-selection statements.

# 8.2.2.3 Implementing Multiple Selection Structures

A multiple selection statement is essentially an n-way branch to segments of code, where n is the number of selectable segments. Implementing such a statement must be done with multiple conditional branch instructions. Consider again the general form of the C switch statement, with breaks:

```
switch (expression) {
  case constant_expression₁: statement₁;
    break;
  ...
  case constantₙ: statementₙ;
    break;
  [default: statementₙ₊₁]
}
```

One simple translation of this statement follows:

```
Code to evaluate expression into t
goto branches
label₁: code for statement₁
  goto out
...
labelₙ: code for statementₙ
  goto out
default: code for statementₙ₊₁
  goto out
branches: if t = constant_expression₁ goto label₁
  ...
  if t = constant_expressionₙ goto labelₙ
  goto default
out:
```