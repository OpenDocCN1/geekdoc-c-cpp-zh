# Flow of Control

> "Would you tell me, please, which way I ought to go from here?"
"That depends a good deal on where you want to get to," said the Cat.
LEWIS CARROLL, Alice in Wonderland

# Introduction

As most programming languages, C++ handles flow of control with branching and looping statements. C++ branching and looping statements are similar to branching and looping statements in other languages. They are the same as they are in the C language and very similar to what they are in the Java programming language. Exception handling is also a way to handle flow of control. Exception handling is covered in Chapter 18.

# 2.1 Boolean Expressions

> He who would distinguish the true from the false must have an adequate idea of what is true and false.
BENEDICT SPINOZA, Ethics

Most branching statements are controlled by Boolean expressions. A Boolean expression is any expression that is either true or false. The simplest for a Boolean expression consists of two expressions, such as numbers or variables, which are compared with one of the comparison operators shown in Display 2.1. Notice that some of the operators are spelled with two symbols, for example, == !=, <=, or >=. Be sure not to use a double equal == for the equal sign and use that the two symbols != for not equal. Two-symbol operators should not have any space between the two symbols.

# Building Boolean Expressions

You can compare two using the "and" operator, which is spelled && in C++. For example, the following Boolean expression is true provided x is greater than 2 and x is less than?:

```
(2 < x) && (x < 7)
```

When two comparisons are connected using &&, the entire expression is true, provided both of the comparisons are true; otherwise, the entire expression is false.