
larger size implementation-defined. That is yet another reason to avoid mixing unsigned and signed integers.

## 10.6 Advice

+ [1] Prefer the standard library to other libraries and to “handcrafted code”; §10.2.8.
+ [2] Use character-level input only when you have to; §10.2.3.
+ [3] When reading, always consider ill-formed input; §10.2.3.
+ [4] Prefer suitable abstractions (classes, algorithms, etc.) to direct use of language features (e.g., int s, statements); §10.2.8.
+ [5] Avoid complicated expressions; §10.3.3.
+ [6] If in doubt about operator precedence, parenthesize; §10.3.3.
+ [7] Avoid expressions with undefined order of evaluation; §10.3.2.
+ [8] Avoid narrowing conversions; §10.5.2.
+ [9] Define symbolic constants to avoid “magic constants”; §10.4.1.
+ [10] Avoid narrowing conversions; §10.5.2.

## 11
## Select Operations

> When someone says “I want a programming language in which I need only say what I wish done,” give him a lollipop.
> — Alan Perlis

- Etc. Operators
- Logical Operators; Bitwise Logical Operators; Conditional Expressions; Increment and Decrement
- Free Store
- Memory Management; Arrays; Getting Memory Space; Overloading new
- Lists
- Implementation Model; Qualified Lists; Unqualified Lists
- Lambda Expressions
- Implementation Model; Alternatives to Lambdas; Capture; Call and Return; The Type of a Lambda
- Explicit Type Conversion
- Construction; Named Casts; C-Style Cast; Function-Style Cast
- Advice

## 11.1 Etc. Operators

This section examines a mixed bag of simple operators: logical operators ( &&, ||, and !), bitwise logical operators (&, |, ^, <<, and >>), conditional expressions (?:), and increment and decrement operators (++ and --). They have little in common beyond their details not fitting elsewhere in the discussions of operators.

### 11.1.1 Logical Operators

The logical operators && (and), || (or), and ! (not) take operands of arithmetic and pointer types, convert them to bool, and return a bool result. The && and || operators evaluate their second argument only if necessary, so they can be used to control evaluation order (§10.3.2). For example:

```
while (p && !whitespace(*p)) ++p;
```

Here, p is not dereferenced if it is the nullptr.

### 11.1.2 Bitwise Logical Operators

The bitwise logical operators & (and), | (or), ^ (exclusive or, xor), ~ (complement), >> (right shift), and << (left shift) are applied to objects of integral types – that is, char, short, int, long, long long and their unsigned counterparts, and bool, wchar_t, char16_t, and char32_t. A plain enum (but not an enum class) can be implicitly converted to an integer type and used as an operand to bitwise logical operations. The usual arithmetic conversions (§10.5.3) determine the type of the result.

A typical use of bitwise logical operators is to implement the notion of a small set (a bit vector). In this case, each bit of an unsigned integer represents one member of the set, and the number of bits limits the number of members. The binary operator & is interpreted as intersection, | as union, ^ as symmetric difference, and ~ as complement. An enumeration can be used to name the members of such a set. Here is a small example borrowed from an implementation of ostream:

```
enum ios_base::iostate {
goodbit=0, eofbit=1, failbit=2, badbit=4
};
```

The implementation of a stream can set and test its state like this:

```
state = goodbit;
// ...
if (state&(badbit|failbit)) // stream not good
```

The extra parentheses are necessary because & has higher precedence than | (§10.3). A function that reaches the end-of-input might report it like this:

```
state |= eofbit;
```

The |= operator is used to add to the state. A simple assignment, state=eofbit, would have cleared all other bits.

These stream state flags are observable from outside the stream implementation. For example, we could see how the states of two streams differ like this:

```
int old = cin.rdstate(); // ... use cin ...
if (cin.rdstate()^old) {
// ...
}
// rdstate() returns the state
// has anything changed?
```

Computing differences of stream states is not common. For other similar types, computing differences is essential. For example, consider comparing a bit vector that represents the set of interrupts being handled with another that represents the set of interrupts waiting to be handled.

Please note that this bit fiddling is taken from the implementation of iostreams rather than from the user interface. Convenient bit manipulation can be very important, but for reliability, maintainability, portability, etc., it should be kept at low levels of a system. For more general notions of a set, see the standard-library set (§31.4.3) and bitset (§34.2.2).

Bitwise logical operations can be used to extract bit-fields from a word. For example, one could extract the middle 16 bits of a 32-bit int like this:

```
constexpr unsigned short middle(int a)
{
static_assert(sizeof(int)==4,"unexpected int size"); static_assert(sizeof(short)==2,"unexpected short size"); return (a>>8)&0xFFFF;
}
```

```
int x = 0xFF00FF00; // assume sizeof(int)==4
short y = middle(x); // y=0x00FF
```

Using fields (§8.2.7) is a convenient shorthand for such shifting and masking.

Do not confuse the bitwise logical operators with the logical operators: &&, ||, and !. The latter return true or false, and they are primarily useful for writing the test in an if-, while-, or for-statement (§9.4, §9.5). For example, !0 (not zero) is the value true, which converts to 1, whereas ~0 (complement of zero) is the bit pattern all-ones, which in two’s complement representation is the value−1.

### 11.1.3 Conditional Expressions

Some if-statements can conveniently be replaced by conditional-expressions. For example:

```
if (a <= b)
max = b;
else
max = a;
```

This is more directly expressed like this:

```
max = (a<=b) ? b : a;
```

The parentheses around the condition are not necessary, but I find the code easier to read when they are used.

Conditional expressions are important in that they can be used in constant expressions (§10.4). A pair of expressions e1 and e2 can be used as alternatives in a conditional expression, c?e1:e2, if they are of the same type or if there is a common type T, to which they can both be implicitly converted. For arithmetic types, the usual arithmetic conversions (§10.5.3) are used to find that common type. For other types, either e1 must be implicitly convertible to e2’s type or vice versa. In addition, one branch may be a throw-expression (§13.5.1). For example:

```
void fct(int * p)
{
int i = (p) ? *p : std::runtime_error{"unexpected nullptr}; // ...
}
```

### 11.1.4 Increment and Decrement

The ++ operator is used to express incrementing directly, rather than expressing it indirectly using a combination of an addition and an assignment. Provided lvalue has no side effects, ++lvalue means lvalue+=1, which again means lvalue=lvalue+1. The expression denoting the object to be incremented is evaluated once (only). Decrementing is similarly expressed by the-- operator.

The operators ++ and-- can be used as both prefix and postfix operators. The value of ++x is the new (that is, incremented) value of x. For example, y=++x is equivalent to y=(x=x+1). The value of x++, however, is the old value of x. For example, y=x++ is equivalent to y=(t=x,x=x+1,t), where t is a variable of the same type as x.

Like adding an int to a pointer, or subtracting it, ++ and-- on a pointer operate in terms of elements of the array into which the pointer points; p++ makes p point to the next element (§7.4.1).

The ++ and-- operators are particularly useful for incrementing and decrementing variables in loops. For example, one can copy a zero-terminated C-style string like this:

```
void cpy(char* p, const char* q)
{
while (*p++ = *q++);
}
```

Like C, C++ is both loved and hated for enabling such terse, expression-oriented coding. Consider: while (*p++ = *q++);

This is more than a little obscure to non-C programmers, but because the style of coding is not uncommon, it is worth examining more closely. Consider first a more traditional way of copying an array of characters:

```
int length = strlen(q);
for (int i = 0; i<=length; i++)
p[i] = q[i];
```

This is wasteful. The length of a zero-terminated string is found by reading the string looking for the terminating zero. Thus, we read the string twice: once to find its length and once to copy it. So we try this instead:

```
int i;
for (i = 0; q[i]!=0 ; i++)
p[i] = q[i];
p[i] = 0; // terminatingzero
```

The variable i used for indexing can be eliminated because p and q are pointers:

```
while ( *q!=0){
*p= *q;
p++; // point to next character
q++; // point to next character
}
*p=0; // terminatingzero
```

Because the post-increment operation allows us first to use the value and then to increment it, we can rewrite the loop like this:

