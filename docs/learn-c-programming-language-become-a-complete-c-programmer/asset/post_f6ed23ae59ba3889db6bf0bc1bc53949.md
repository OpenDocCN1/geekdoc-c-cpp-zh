
The definition of **Token** looks like this:

```
enum class Kind : char {
name, number, end,
plus='+', minus='-', mul='*', div='/', print=';', assign='=', lp='(', rp=')'
};

struct Token {
Kind kind;
string string_value;
double number_value;
};
```

Representing each token by the integer value of its character is convenient and efficient and can be a help to people using debuggers. This works as long as no character used as input has a value used as an enumerator – and no current character set I know of has a printing character with a single-digit integer value.

The interface to **Token_stream** looks like this:

```
class Token_stream {
public:
Token get();
const Token& current();
// ...
};
```

```
// read and return next token // most recently read token
```

The implementation is presented in §10.2.2.

Each parser function takes a **bool** (§6.2.2) argument, called **get**, indicating whether the function needs to call **Token_stream::get()** to get the next token. Each parser function evaluates “its” expression and returns the value. The function **expr()** handles addition and subtraction. It consists of a single loop that looks for terms to add or subtract:

```
double expr(bool get) {
double left = term(get);
// add and subtract
for (;;) { // “forever”

switch (ts.current().kind) {
case Kind::plus:
left += term(true);
break;
case Kind::minus:
left -= term(true);
break;
default:
return left;
}
}
}
```

This function really does not do much itself. In a manner typical of higher-level functions in a large program, it calls other functions to do the work.

The **switch**-statement (§2.2.4, §9.4.2) tests the value of its condition, which is supplied in parentheses after the **switch** keyword, against a set of constants. The **break**-statements are used to exit the **switch**-statement. If the value tested does not match any **case** label, the **default** is chosen. The programmer need not provide a **default**.

Note that an expression such as 2−3+4 is evaluated as (2−3)+4, as specified in the grammar. The curious notation for(; ;) is a way to specify an infinite loop; you could pronounce it “forever” (§9.5); **while(true)** is an alternative. The **switch**-statement is executed repeatedly until something different from + and− is found, and then the **return**-statement in the default case is executed.

The operators += and−= are used to handle the addition and subtraction; **left=left+term(true)** and **left=left−term(true)** could have been used without changing the meaning of the program. However, **left+=term(true)** and **left−=term(true)** are not only shorter but also express the intended operation directly. Each assignment operator is a separate lexical token, so **a+=1;** is a syntax error because of the space between the + and the =.

C++ provides assignment operators for the binary operators:

```
+ - * / % & | ^ << >>
```

so that the following assignment operators are possible:

```
+= -= *= /= %= &= |= ^= <<= >>=
```

The **%** is the modulo, or remainder, operator; **&**, **|**, and **^** are the bitwise logical operators and, or, and exclusive or; **<<** and **>>** are the left shift and right shift operators; §10.3 summarizes the operators and their meanings. For a binary operator @ applied to operands of built-in types, an expression **x@=y** means **x=x@y**, except that **x** is evaluated once only.

The function **term()** handles multiplication and division in the same way **expr()** handles addition and subtraction:

```
double term(bool get) // multiply and divide
{
double left = prim(get);
for (;;) {
switch (ts.current().kind) {
case Kind::mul:

left *= prim(true);
break;
case Kind::div:

if (auto d = prim(true)) {
left /= d;
break;
}
return error("divide by 0");
default:
return left;
}
}
}
```

The result of dividing by zero is undefined and usually disastrous. We therefore test for 0 before dividing and call error() if we detect a zero divisor. The function error() is described in §10.2.4.

The variable d is introduced into the program exactly where it is needed and initialized immediately. The scope of a name introduced in a condition is the statement controlled by that condition, and the resulting value is the value of the condition (§9.4.3). Consequently, the division and assignment left/=d are done if and only if d is nonzero.

The function prim() handling a primary is much like expr() and term(), except that because we are getting lower in the call hierarchy a bit of real work is being done and no loop is necessary:

```
double prim(bool get) // handle primaries {
if (get) ts.get(); // read next token

switch (ts.current().kind) {
case Kind::number: // floating-point constant { double v = ts.current().number_value;
ts.get();
return v;
}
case Kind::name:
{ double& v = table[ts.current().string_value]; if (ts.get().kind == Kind::assign) v = expr(true); return v;
}

// find the corresponding // ' = ' seen: assignment

case Kind::minus: // unary minus
return -prim(true);
case Kind::lp:
{ auto e = expr(true);
if (ts.current().kind != Kind::rp) return error("')' expected");
ts.get(); // eat ')'
return e;
}
default:
return error("primary expected");
}
}
```

When a Token that is a number (that is, an integer or floating-point literal) is seen, its value is placed in its number_value. Similarly, when a Token that is a name (however defined; see §10.2.2 and §10.2.3) is seen, its value is placed in its string_value.

Note that prim() always reads one more Token than it uses to analyze its primary expression. The reason is that it must do that in some cases (e.g., to see if a name is assigned to), so for consistency it must do it in all cases. In the cases where a parser function simply wants to move ahead to the next Token, it doesn’t use the return value from ts.get(). That’s fine because we can get the result from ts.current(). Had ignoring the return value of get() bothered me, I’d have either added a read() function that just updated current() without returning a value or explicitly “thrown away” the result: void(ts.get()).

Before doing anything to a name, the calculator must first look ahead to see if it is being assigned to or simply read. In both cases, the symbol table is consulted. The symbol table is a map (§4.4.3, §31.4.3):

```
map<string,double> table;
```

That is, when table is indexed by a string, the resulting value is the double corresponding to the string. For example, if the user enters

```
radius = 6378.388;
```

the calculator will reach case Kind::name and execute

```
double& v = table["radius"];
// ... expr() calculates the value to be assigned ...
v = 6378.388;
```

The reference v is used to hold on to the double associated with radius while expr() calculates the value 6378.388 from the input characters.

Chapter 14 and Chapter 15 discuss how to organize a program as a set of modules. However, with one exception, the declarations for this calculator example can be ordered so that everything is declared exactly once and before it is used. The exception is expr(), which calls term(), which calls prim(), which in turn calls expr(). This loop of calls must be broken somehow. A declaration

```
double expr(bool);
```

before the definition of prim() will do nicely.

## 10.2.2 Input

Reading input is often the messiest part of a program. To communicate with a person, the program must cope with that person’s whims, conventions, and seemingly random errors. Trying to force the person to behave in a manner more suitable for the machine is often (rightly) considered offensive. The task of a low-level input routine is to read characters and compose higher-level tokens from them. These tokens are then the units of input for higher-level routines. Here, low-level input is done by ts.get(). Writing a low-level input routine need not be an everyday task. Many systems provide standard functions for this.

First we need to see the complete definition of Token_stream:

```
class Token_stream {
```
