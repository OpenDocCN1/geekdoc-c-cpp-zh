# 3.8 Arithmetic 127

this chapter's exercises and in later chapters, we consider several interesting applications of the remainder operator, as determining whether one is a multiple of another.

# 3.8.1 Arithmetic Expressions in Straight-Line Form

Arithmetic expressions must be written in straight-line form to facilitate entering an app's code into the computer. Thus, expressions such as “a divided by b” must be written as a / b in a straight line. The following algebraic notation is not acceptable to the C# compiler and cannot be typed into the Visual Studio editor:

```
a
b
```

# 3.8.2 Parentheses for Grouping Subexpressions

Parentheses are used to group terms in C# expressions in the same manner as in algebraic expressions. For example, to multiply times the quantity b + c, we write

```
a * (b + c)
```

If an expression contains nested parentheses, such as

```
(a + b) * c
```

the expression in the innermost set of parentheses (a + b in this case) is evaluated first.

# 3.8.3 Rules of Operator Precedence

C# applies the operators in arithmetic expressions in a precise sequence determined by the following rules of operator precedence, which are generally the same as those followed in algebra (Fig. 3.19). These rules enable C# to apply operators in the correct order.^4

| Operators | Operations | Order of evaluation (associativity) |
| --- | --- | --- |
| Evaluated first | | If there are several operators of this type, they're evaluated from left to right. |
| * | Multiplication | |
| / | Division | |
| % | Remainder | |
| Evaluated next | | If there are several operators of this type, they're evaluated from left to right. |
| + | Addition | |
| - | Subtraction | |

**Fig. 3.19** Precedence of arithmetic operators.

When we say operators are applied from left to right, we're referring to their associativity. You'll see some operators operate from left to right. Figure 3.19 summa

+   4. We discuss simple examples to explain the order of evaluation. More subtle order of evaluation issues occur in the increasingly complex expressions you'll encounter. For more details, see the following blog post from Eric Lippert: https://ericlippet.com/2008/05/23/ and https://ericlippert.com/2007/08/14/