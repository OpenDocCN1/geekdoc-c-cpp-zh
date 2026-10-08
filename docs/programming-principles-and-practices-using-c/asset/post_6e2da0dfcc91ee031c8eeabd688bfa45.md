
Basically, we replaced `keep_window_open()` with our own code. Note that we still have our problem if a `~` happens to be a character to be read after an error, but that's rather unlikely.

When we encountered this problem we wrote a version of `keep_window_open()` that takes a string as its argument and closes the window only when you enter that string after getting the prompt, so a simpler solution is

```cpp
catch (runtime_error& e) {
    cerr << e.what() << '\n';
    keep_window_open("~~");
    return 1;
}
```

Now examples such as

```
+1
!1~~
()
```

will cause the calculator to give the proper error messages, then say

`Please enter ~~ to exit`

and not exit until you enter the string `~~`.

The calculator takes input from the keyboard. That makes testing tedious: each time we make an improvement, we have to type in a lot of test cases (yet again!) to make sure we haven't broken anything. It would be much better if we could store our test cases somewhere and run them with a single command. Some operating systems (notably Unix) make it trivial to get `cin` to read from a file without modifying the program, and similarly to divert the output from `cout` to a file. If that's not convenient, we must modify the program to use a file (see Chapter 10).

Now consider:

`1+2; q`

and

`1+2 q`

We would like both to print the result `(3)` and then exit the program. Curiously enough,

`1+2 q`

does that, but the apparently cleaner

`1+2; q`

elicits a **Primary expected** error. Where would we look for this error? In **main()** where `;` and **q** are handled, of course. We added those “print” and “quit” commands rather quickly to get the calculator to work (§6.7). Now we are paying for that haste. Consider again:

```cpp
double val = 0;
while (cin) {
    cout << "> ";
    Token t = ts.get();
    if (t.kind == 'q') break;
    if (t.kind == ';')
        cout << "= " << val << "\n";
    else {
        ts.putback(t);
        val = expression();
    }
}
```

If we find a semicolon, we straightaway proceed to call **expression()** without checking for **q**. The first thing that **expression()** does is to call **term()**, which first calls **primary()**, which finds **q**. The letter **q** isn’t a **Primary** so we get our error message. So, we should test for **q** after testing for a semicolon. While we were at it, we felt the need to simplify the logic a bit, so the complete **main()** reads

```cpp
int main()
try
{
    while (cin) {
        cout << "> ";
        Token t = ts.get();
        while (t.kind == ';') t = ts.get(); // eat ';'
        if (t.kind == 'q') {
            keep_window_open();
            return 0;
        }
        ts.putback(t);
        cout << "= " << expression() << "\n";
    }
    keep_window_open();
    return 0;
}
catch (exception& e) {
    cerr << e.what() << "\n";
    keep_window_open("~~");
    return 1;
}
catch (...) {
    cerr << "exception \n";
    keep_window_open("~~");
    return 2;
}
```

This makes for reasonably robust error handling. So we can start considering what else we can do to improve the calculator.

### 7.4 Negative numbers

If you tested the calculator, you found that it couldn't handle negative numbers elegantly. For example, this is an error:

`-1/2`

We have to write

`(0-1)/2`

That's not acceptable.

Finding such problems during late debugging and testing is common. Only now do we have the opportunity to see what our design really does and get the feedback that allows us to refine our ideas. When planning a project, it is wise to try to preserve time and flexibility to benefit from the lessons we learn here. All too often, “release 1.0” is shipped without needed refinements because a tight schedule or a rigid project management strategy prevents “late” changes to the specification; “late” addition of “features” is especially dreaded. In reality, when a program is good enough for simple use by its designers but not yet ready to ship, it isn't “late” in the development sequence; it's the earliest time when we can benefit from solid experience with the program. A realistic schedule takes that into account.

In this case, we basically need to modify the grammar to allow unary minus. The simplest change seems to be in **Primary**. We have

```
Primary:
    Number
    "(" Expression ")"
```

and we need something like

```
Primary:
    Number
    "(" Expression ")"
    "-" Primary
    "+" Primary
```

We added unary plus because that's what C++ does. When we have unary minus, someone always tries unary plus and it's easier just to implement that than to explain why it is useless. The code that implements Primary becomes

```cpp
double primary()
{
    Token t = ts.get();
    switch (t.kind) {
        case '(':	// handle '(' expression ')'
            {
                double d = expression();
                t = ts.get();
                if (t.kind != ')') error("')' expected");
                return d;
            }
        case '8':		// we use '8' to represent a number
            return t.value;	// return the number's value
        case '-':
            return - primary();
        case '+':
            return primary();
        default:
            error("primary expected");
    }
}
```

That's so simple that it actually worked the first time.

### 7.5 Remainder: %

When we first analyzed the ideals for a calculator, we wanted the remainder (modulo) operator: %. However, % is not defined for floating-point numbers, so we backed off. Now we can consider it again. It should be simple:

1.  We add % as a Token.
2.  We define a meaning for %.

We know the meaning of `%` for integer operands. For example:

```
> 2%3;
= 2
> 3%2;
= 1
> 5%3;
= 2
```

But how should we handle operands that are not integers? Consider:

```
> 6.7%3.3;
```

What should be the resulting value? There is no perfect technical answer. However, modulo is often defined for floating-point operands. In particular, `x%y` can be defined as `x%y==x-y*int(x/y)`, so that `6.7%3.3==6.7-3.3*int(6.7/3.3)`, that is, `0.1`. This is easily done using the standard library function `fmod()` (floating-point modulo) from `<cmath>` (§24.8). We modify `term()` to include

```cpp
        case '%':
        {
            double d = primary();
            if (d == 0) error("%: divide by zero");
            left = fmod(left,d);
            t = ts.get();
            break;
        }
```

The `<cmath>` library is where we find all of the standard mathematical functions, such as `sqrt(x)` (square root of x), `abs(x)` (absolute value of x), `log(x)` (natural logarithm of x), and `pow(x,e)` (x to the power of e).

Alternatively, we can prohibit the use of `%` on a floating-point argument. We check if the floating-point operands have fractional parts and give an error message if they do. The problem of ensuring `int` operands for `%` is a variant of the narrowing problem (§3.9.2 and §5.6.4), so we could solve it using `narrow_cast`:

```cpp
        case '%':
        {
            int i1 = narrow_cast<int>(left);
            int i2 = narrow_cast<int>(primary());
            if (i2 == 0) error("%: divide by zero");
            left = i1%i2;
            t = ts.get();
            break;
        }
```

For a simple calculator, either solution will do.

### 7.6 Cleaning up the code

We have made several changes to the code. They are, we think, all improvements, but the code is beginning to look a bit messy. Now is a good time to review the code to see if we can make it clearer and shorter, add and improve comments, etc. In other words, we are not finished with the program until we have it in a state suitable for someone else to take over maintenance. Except for the almost total absence of comments, the calculator code really isn't that bad, but let's do a bit of cleanup.

#### 7.6.1 Symbolic constants

Looking back, we find the use of `'8'` to indicate a **Token** containing a numeric value odd. It doesn't really matter what value is used to indicate a number **Token** as long as the value is distinct from all other values indicating different kinds of **Tokens**. However, the code looks a bit odd and we had to keep reminding ourselves in comments:

```cpp
case '8':                // we use '8' to represent a number
    return t.value;      // return the number's value
case '-':
    return -primary();
```

To be honest, we also made a few mistakes, typing `'0'` rather than `'8'`, because we forgot which value we had chosen to use. In other words, using `'8'` directly in the code manipulating **Tokens** was sloppy, hard to remember, and error-prone; `'8'` is one of those “magic constants” we warned against in §4.3.1. What we should have done was to introduce a symbolic name for the constant we used to represent a number:

```cpp
const char number = '8';    // t.kind==number means that t is a number Token
```

The **const** modifier simply tells the compiler that we are defining an object that is not supposed to change: for example, an assignment **number=“0”** would cause the compiler to give an error message. Given that definition of **number**, we don't have to use `'8'` explicitly anymore. The code fragment from **primary** above now becomes

```cpp
case number:
    return t.value;      // return the number's value
case '-':
    return -primary();
```

This requires no comment. We should not say in comments what can be clearly and directly said in code. Repeated comments explaining something are often an indication that the code should be improved.
