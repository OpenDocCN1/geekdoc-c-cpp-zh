# ### 3.1.1 Primary Expressions

A **primary expression** is a simple expression with no operator. It is the basic building block for making more complex expressions. A primary expression has precedence 19, which means it has the highest precedence among all expressions. We have several primary expressions, as shown in Appendix C, but we describe only those shown in Table 3.1.

# ### Literal

We have discussed *literals* (values that are used in a program). A *literal* in a program is a primary expression; it has a value, but no side-effect. The following shows some literals as primary expressions. Note that there are no short literals.

| Literal | Description | Literal | Description |
|---|---|---|---|
| `false` | `// Boolean literal` | `12897234L` | `// long integer literal` |
| `'A'` | `// character literal` | `245.78F` | `// float literal` |
| `"Hello"` | `// string literal` | `114.7892` | `// double literal` |
| `234` | `// integer literal` | `245.784321L` | `// long double literal` |

# ### EXAMPLE 3.1

As we have seen, a literal can be used for the sake of its value, as shown in Program 3.1.

# ### Name

When we use a **name** in our program we are using a primary expression. An *identifier* as a name can be a variable, an object name, a function name, and so on. The simplest name we can use in our program is the name of a variable. It is a primary expression with a value, the

# **Program 3.1** Literal expressions

```
```cpp
/************************************************************
 * The program shows some literal expressions.
 ************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    cout << false << " " << 'A' << " " << "Hello" << endl;
    cout << 23412 << " " << 12897234L << endl;
    cout << 245.78F << " " << 114.782 << " " << 2.051L;
    return 0;
}
```

**Run:**
```text
0 A Hello                 // A Boolean, a character, a string
23412 12897234            // An integer, a long integer (there is no short literal)
24.78 114.782 2.051      // A float, a double, a long double
```
```