In spite of the problems side effects cause in expression evaluation, sometimes expressions are explicitly constructed with side effects in mind. For example, in C, assignment (a quintessential side effect) is an expression, not a statement: x = y not only assigns the value of y to x but also returns the copied value as its result.³ Thus, assignments can be combined in expressions, so that

```
x = (y = z)
```

assigns the value of z to both x and y. Note that in languages with this kind of construction, assignment can be considered to be a binary operator similar to arithmetic operators. In that case its precedence is usually lower than other binary operators, and it is made right associative. Thus,

```
x = y = z + w
```

in C assigns the sum of z and w to both x and y (and returns that value as its result).

C and other expression languages also have a **sequence operator**, which allows several expressions to be combined into a single expression and evaluated sequentially. In C, the sequence operator is the comma operator, which has precedence lower than any other operator. Unlike most other operators in C, the order of evaluation is specified as left to right, and the value of the rightmost expression is the value returned by the entire expression. For example, given that x and y are integer variables with values 1 and 2, respectively, the C expression

```
x = (y+=1, x+=y, x+1)
```

returns the value 5 and leaves x with the value 5 and y with the value 3.

The evaluation of an expression can sometimes be performed even without the evaluation of all its subexpressions. An interesting case is that of the Boolean, or logical, expressions. For example, the Boolean expressions (in Ada or C++ syntax)

```
true or x
```

and

```
x or true
```

are true regardless of whether x is true or false. Similarly,

```
false and x
```

and

```
x and false
```

are clearly false regardless of the value of x. In a programming language, one can specify that Boolean expressions are to be evaluated in left-to-right order, up to the point where the truth value of the entire expression becomes known and then the evaluation stops. A programming language that has this rule is said to possess **short-circuit evaluation** of Boolean or logical expressions.

> ³When a type conversion occurs, the type of the copied value is that of x, not y.