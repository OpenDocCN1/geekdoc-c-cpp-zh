+   - `x==10 || y==5`
+   - `!a`

+   - **Bitwise expressions** – Refer to expressions that are used to manipulate data at bit level. They are used for testing and shifting bits. Following are some examples of bitwise expressions:
+     - `x << 3        //Shift 3 bit positions to the left`
+     - `y >> 1        //Shift 1 bit position to the right`

Shift operators are often used for multiplication and division by powers of two. Now, let's learn about the operators in C++.

# ## Operators

All the C operators are also valid in C++. In addition to these operators, C++ has introduced some new operators; for example, the insertion (<<) and extraction (>>) operators, which we have already seen in the previous sections. Let's now learn about the new built-in operators in C++, given as follows:

+   - **Scope Resolution Operator (::)** – C++ is a block-structured language, as blocks and scopes are used in constructing C++ programs. As we know, variables with the same name can be used with different meaning in various blocks of code. The scope of a variable extends from the point of its declaration till the end of the block containing it. A variable declared inside a block is said to be local to that block. Consider the following code snippet:

```
...
{
    int x = 10;
    ...
}
...
{
    int x = 101;
    ...
}
...
```

In the preceding code snippet, we have defined two x variables but within different scopes. These two variables have different memory locations containing different values. Statements in the second block cannot refer to the x variable in the first block or vice versa.

Consider a situation where we are working with a local variable named my_account; however, we also want to access one of the global variables defined with the same name, my_account, from the local scope. In C, we cannot access a global variable with the same name as that of the local variable from within a scope, but C++ allows us to do so using the scope resolution operator. Following is the syntax to use the scope resolution operator:

```
:: variable_name
```

The following program demonstrates the use of scope resolution operator in C++:

```
1: //Demonstrate scope resolution operation in C++
2: #include <iostream>
3: using namespace std;
4:
5: int my_account;        //Global variable definition
6:
7: int main()
8: {
9:     my_account = 9001;
```