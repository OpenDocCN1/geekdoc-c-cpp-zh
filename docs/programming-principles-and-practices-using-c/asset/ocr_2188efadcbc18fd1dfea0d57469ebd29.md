You can't divide by zero. If you try, the computer hardware will detect it and terminate your program with a somewhat unhelpful error message. An inexperienced programmer will discover this the hard way. So, we'd better check and give a decent error message:

```
```
double term()
{
    double left = primary();
    Token t = get_token();
    while (true) {
        switch (t.kind) {
            case 1*':
                left *= primary();
                t = get_token();
                break;
            case 1/':
                {
                    double d = primary();
                    if (d == 0) error("divide by zero");
                    left /= d;
                    t = get_token();
                    break;
                }
            default:
                return left;
        }
    }
}
```
```

Why did we put the statements handling / into a block? The compiler insists. If you want to define and initialize variables within a **switch**\-statement, you must place them inside a block.

# ### 6.5.4 Primary expressions

The grammar rule for primary expressions is also simple:

```
```
Primary:
    Number
    '(' Expression ')'
```
```

The code that implements it is a bit messy because there are more opportunities for syntax errors: