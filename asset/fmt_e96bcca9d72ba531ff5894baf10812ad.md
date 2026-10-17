
A `char` variable is of the natural size to hold a character on a given machine (typically an 8-bit byte), and the sizes of other types are quoted in multiples of the size of a `char`. The size of a type is implementation-defined (i.e., it can vary among different machines) and can be obtained by the `sizeof` operator; for example, `sizeof(char)` equals `1` and `sizeof(int)` is often `4`.

The arithmetic operators can be used for appropriate combinations of these types:

### Section 2.2.2 Types, Variables, and Arithmetic

```
x+y // plus
+x // unary plus
x-y // minus
-x // unary minus
x*y // multiply
x/y // divide
x%y // remainder (modulus) for integers
```

So can the comparison operators:

```
x==y // equal
x!=y // not equal
x<y // less than
x>y // greater than
x<=y // less than or equal
x>=y // greater than or equal
```

In assignments and in arithmetic operations, C++ performs all meaningful conversions (§10.5.3) between the basic types so that they can be mixed freely:

```
void some_function() {
// function that doesn’t return a value
double d = 2.2; int i = 7;
// initialize floating-point number
// initialize integer
d = d+i; // assign sum to d
i=d*i; // assign product to i (truncating the double d*i to an int)
}
```

Note that `=` is the assignment operator and `==` tests equality.

C++ offers a variety of notations for expressing initialization, such as the `=` used above, and a universal form based on curly-brace-delimited initializer lists:

```
double d1 = 2.3; double d2 {2.3};
complex<double> z = 1; complex<double> z2 {d1,d2}; complex<double> z3 = {1,2};
// a complex number with double-precision floating-point scalars
// the = is optional with { ... }
vector<int> v {1,2,3,4,5,6}; // a vector of ints
```

The `=` form is traditional and dates back to C, but if in doubt, use the general `{}-list` form (§6.3.5.2). If nothing else, it saves you from conversions that lose information (narrowing conversions; §10.5):

```
int i1 = 7.2; // i1 becomes 7
int i2 {7.2}; // error :floating-point to integer conversion
int i3 = {7.2}; // error :floating-point to integer conversion (the = is redundant)
```

A constant (§2.2.3) cannot be left uninitialized and a variable should only be left uninitialized in extremely rare circumstances. Don’t introduce a name until you have a suitable value for it. Userdefined types (such as `string`, `vector`, `Matrix`, `Motor_controller`, and `Orc_warrior`) can be defined to be implicitly initialized (§3.2.1.1).

When defining a variable, you don’t actually need to state its type explicitly when it can be deduced from the initializer:

```
auto b = true; auto ch = ‘x’; auto i = 123;
auto d = 1.2;
auto z = sqrt(y);
// a bool
// a char
// an int
// a double
// z has the type of whatever sqrt(y) returns
```

With `auto`, we use the `=` syntax because there is no type conversion involved that might cause problems (§6.3.6.2).

We use `auto` where we don’t have a specific reason to mention the type explicitly.

“Specific reasons” include:

- The definition is in a large scope where we want to make the type clearly visible to readers of our code.

- We want to be explicit about a variable’s range or precision (e.g., `double` rather than `float`). Using `auto`, we avoid redundancy and writing long type names. This is especially important in generic programming where the exact type of an object can be hard for the programmer to know and the type names can be quite long (§4.5.1).

In addition to the conventional arithmetic and logical operators (§10.3), C++ offers more specific operations for modifying a variable:

```
x+=y // x=x+y
++x // increment: x = x+1
x-=y // x=x-y
--x // decrement: x = x-1
x*=y // scaling: x = x*y
x/=y // scaling: x = x/y
x%=y // x=x%y
```

These operators are concise, convenient, and very frequently used.

### 2.2.3 Constants

C++ supports two notions of immutability (§7.5):

- `const`: meaning roughly “I promise not to change this value” (§7.5). This is used primarily to specify interfaces, so that data can be passed to functions without fear of it being modified. The compiler enforces the promise made by `const`.

- `constexpr`: meaning roughly “to be evaluated at compile time” (§10.4). This is used primarily to specify constants, to allow placement of data in memory where it is unlikely to be corrupted, and for performance.

For example:

```
const int dmv = 17;
int var = 17;
// dmv is a named constant
// var is not a constant
constexpr double max1 = 1.4*square(dmv); // OK if square(17) is a constant expression
constexpr double max2 = 1.4*square(var); // error :var is not a constant expression
const double max3 = 1.4*square(var); // OK, maybe evaluated at run time
```

```
double sum(const vector<double>&);
vector<double> v {1.2, 3.4, 4.5};
const double s1 = sum(v); // OK: evaluated at run time
constexpr double s2 = sum(v); // error :sum(v) not constant expression
// sum will not modify its argument (§2.2.5)
// v is not a constant
```

For a function to be usable in a constant expression, that is, in an expression that will be evaluated by the compiler, it must be defined `constexpr`. For example:

```
constexpr double square(double x) { return x *x; }
```

To be `constexpr`, a function must be rather simple: just a `return`-statement computing a value. A `constexpr` function can be used for non-constant arguments, but when that is done the result is not a constant expression. We allow a `constexpr` function to be called with non-constant-expression arguments in contexts that do not require constant expressions, so that we don’t have to define essentially the same function twice: once for constant expressions and once for variables.

In a few places, constant expressions are required by language rules (e.g., array bounds (§2.2.5, §7.3), `case` labels (§2.2.4, §9.4.2), some template arguments (§25.2), and constants declared using `constexpr`). In other cases, compile-time evaluation is important for performance. Independently of performance issues, the notion of immutability (of an object with an unchangeable state) is an important design concern (§10.4).

### 2.2.4 Tests and Loops

C++ provides a conventional set of statements for expressing selection and looping. For example, here is a simple function that prompts the user and returns a Boolean indicating the response:

```
bool accept() {
cout << "Do you want to proceed (y or n)?\n"; // writequestion
char answer = 0; cin >> answer; // read answer
if (answer == ‘y’) return true; return false;
}
```

To match the `<<` output operator (“put to”), the `>>` operator (“get from”) is used for input; `cin` is the standard input stream. The type of the right-hand operand of `>>` determines what input is accepted, and its right-hand operand is the target of the input operation. The `\n` character at the end of the output string represents a newline (§2.2.1).

The example could be improved by taking an `n` (for “no”) answer into account:

```
bool accept2() {
cout << "Do you want to proceed (y or n)?\n"; // writequestion
char answer = 0; cin >> answer; // read answer
switch (answer) {
case ‘y’:
return true;

case ‘n’:
return false;
default:
cout << "I’ll take that for a no.\n";
return false;
}
}
```

A `switch`-statement tests a value against a set of constants. The `case` constants must be distinct, and if the value tested does not match any of them, the `default` is chosen. If no `default` is provided, no action is taken if the value doesn’t match any `case` constant.

很少有程序不用循环就能写成。例如，我们可能希望给用户几次机会来输入可接受的输入：

```
bool accept3()
{
int tries = 1;
while (tries<4) {
cout << "Do you want to proceed (y or n)?\n"; char answer = 0;
cin >> answer;

// writequestion
// read answer
switch (answer) {
case 'y':
return true;

case 'n':
return false;
default:
cout << "Sorry, I don't understand that.\n"; ++tries; // increment
}
}
cout << "I'll take that for a no.\n";
return false;
}
```

`while`语句会一直执行，直到其条件变为`false`。

### 2.2.5 指针、数组和循环

可以这样声明一个元素类型为`char`的数组：
