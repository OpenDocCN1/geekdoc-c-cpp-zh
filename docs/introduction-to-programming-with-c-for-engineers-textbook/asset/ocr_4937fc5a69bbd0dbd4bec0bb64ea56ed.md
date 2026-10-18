# ## 3.19.2 Further Notes on Operators

Be careful not to assume any special evaluation order for subexpressions. For example, the following dependencies should be avoided:

```
```
int f( int & x )
{
    return x += 2;
}

int g( int & x )
{
    return x *= 3;
}

void h( void )
{
    int x = 10;
    int p = f( x ) + g( x ); // can be 48 or 42
    // ...
}
```
```

The result of `p` can be different depending on whether `f` is called before `g` or `g` before `f`, which is not defined in the C++ standard. On the other hand, the logical operators `&&` (and) and `||` (or), as well as `,` (comma), guarantee that the left-hand operation is performed before the right-hand operation. For example,

```
```
f( x ) && g( x )
```
```

is guaranteed to call function `f` before `g`. But for built-in types, the `&&` operator's second operand is _not_ evaluated if the first operand has been evaluated to `false` (since the result is obviously `false` in such a case). Similarly, the `||` operator's second operand is evaluated only if the first one returned `false` (this is known as short-circuit evaluation). This is especially useful to check for null pointers before accessing objects, as in the following function:

```
```
bool check_if_not_empty_string( char * p )
{
    // the second cond is evaluated only if first is true
    if( p != nullptr && * p != 0 )
        return true;
    else
        return false;
}
```
```

In this `if` statement, the pointer `p` is first checked to see if it is a null pointer (denoted by `0` in C/ C++ or `nullptr` in C++11). If it is `nullptr`, then we cannot evaluate its dereferencing expression `* p`, since it would throw a software exception. However, if `p` is a valid pointer, we check the first letter of the text pointed to by `p`; if it is not zero, we return `true` to indicate that the text is not empty. Otherwise, we return `false`.

Since this short-circuit evaluation feature is guaranteed _only_ for the built-in types, we cannot rely on it if we call a class's overloaded `&&` and `||` operators. Therefore, if we really need to overload these operators, we should do so carefully (Section 4.4).