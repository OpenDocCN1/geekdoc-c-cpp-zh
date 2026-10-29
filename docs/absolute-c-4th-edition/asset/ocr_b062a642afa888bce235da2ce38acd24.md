# Flow of Control

> > “Would you tell me, please, which way I ought to go from here?”
> > “That depends a good deal on where you want to get to,” said the Cat.
> >
> > — Lewis Carroll, *Alice in Wonderland*

# INTRODUCTION

As in most programming languages, C++ handles flow of control with branching and looping statements. C++ branching and looping statements are similar to branching and looping statements in other languages. They are the same as in the C language and very similar to what they are in the Java programming language. Exception handling is also a way to handle flow of control. Exception handling is covered in Chapter 18.

# 2.1 Boolean Expressions

> > He who would distinguish the true from the false must have an adequate idea of what is true and false.
> >
> > — Benedict Spinoza, *Ethics*

Most branching statements are controlled by Boolean expressions. A **Boolean expression** is any expression that is either true or false. The simplest form for a Boolean expression consists of two expressions, such as numbers or variables, that are compared with one of the comparison operators shown in Display 2.1. Notice that some of the operators are spelled with two symbols, for example, ==, !=, <=, >=. Be sure to notice that you use a double equal sign for the equal sign and that you use the two symbols != for not equal. Such two-symbol operators should not have any space between the two symbols.

# BUILDING BOOLEAN EXPRESSIONS

You can combine two comparisons using the “and” operator, which is spelled && in C++. For example, the following Boolean expression is true provided x is greater than 2 and x is less than 7:

```
`(2 < x) && (x < 7)`
```

When two comparisons are connected using a &&, the entire expression is true, provided both of the comparisons are true; otherwise, the entire expression is false.