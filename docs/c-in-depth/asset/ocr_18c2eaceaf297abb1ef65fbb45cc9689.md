```
switch(expression)
{
  case constant1:
    statement
    ........
  case constant2:
    statement
    ........
    ..........
    ..........
  case constantN:
    statement
    ........
  default :
    statement
    ........
}
```

Here switch, case and default are keywords. The "expression" following the switch keyword can be any C expression that yields an integer value. It can be value of any integer or character variable, or a function call returning an integer, or an arithmetic, logical, relational, bitwise expression yielding an integer. It can be any integer or character constant also. Since characters are converted to their ASCII values, so we can also use characters in this expression. Data types long int and short int are also allowed.

The constants following the case keywords should be of integer or character type. They can be either constants or constant expressions. These constants must be different from one another.

We can't use floating point or string constants. Multiple constants in a single case are not allowed; each case should be followed by only one constant.

Each case can be followed by any number of statements. It is also possible that a case has no statement under it. If a case is followed by multiple statements, then it is not necessary to enclose them within pair of curly braces, but it is not an error if we do so. The statements under case can be any valid C statements like if else, while, for or even another switch statement. Writing a switch statement inside another is called nesting of switches. Now we'll see some valid and invalid ways of writing switch expressions and case constants.

int a, b, c; char d, e; float f;

# Valid

```
switch(a) switch(a>b) switch(d +e-3) switch(a>b && b>c) switch(func(a, b))
```

# Invalid

switch(f) switch(a+4.5)

# Valid

case 4: case 'a': case 2+4: case 'a'>'b':

# Invalid

case "second": case 2.3: case a: case a>b: case a+2: case 2, 4, 5: case 2 4 : 4 : 5 :

Now let us see how the switch statement works. Firstly the switch expression is evaluated, then the