
in Stroustrup [1997], and ML’s type system in Ullman [1998] and Harper and Mitchell [1993]; Haskell’s in Thompson [1999].

For a study of type polymorphism and overloading, see Cardelli and Wegner [1985]. The Hindley-Milner algorithm is clearly presented in Cardelli [1987], together with Modula-2 code that implements it for a small sample language; let-bound polymorphism and the occur-check are also discussed. Let-bound polymorphism is also described in Ullman [1998], Section 5.3, where “generic” type variables are called “generalizable.” C++ templates are amply described in Stroustrup [1997]. Ada “generics” are described in Cohen [1996]. Polymorphic recursion (Exercise 9.38) is described in Henglein [1993].

The IEEE floating-point standard, mentioned in Section 8.2, appears in IEEE [1985].

## CHAPTER

## Control I—Expressions
and Statements

- 9.1    Expressions    403
- 9.2    Conditional Statements and Guards    410
- 9.3    Loops and Variations on WHILE    417
- 9.4    The GOTO Controversy and Loop Exits    420
- 9.5    Exception Handling    423
- 9.6    Case Study: Computing the Values of Static Expressions in TinyAda    432

## CHAPTER 9

In Chapter 8, we discussed basic and structured abstraction of data through the use of data types. In this chapter, we discuss the basic and structured abstraction of control through the use of expressions and statements. Structured control through the use of procedures and functions, and the organization of runtime environments, will be studied in the next chapter. As noted in Chapter 1, unit-level data and control converge to the same kinds of language mechanisms, and they will be studied in the chapter on modules.

Expressions represent the most fundamental computation mechanism in programs. An **expression**, in its pure, mathematical, form, returns a value and produces no side effect. That is, it does not change program memory. By contrast, a **statement** is executed for its side effects and returns no value. Many languages, however, do not make such a clear distinction and allow expressions to contain side effects. In functional languages—sometimes also called **expression languages**—virtually all language constructs are expressions. Even in nonfunctional languages, expressions play a significant role, and in some languages, such as C (which could be called an **expression-oriented language**), expressions make up a much larger portion of the language than statements. Expressions are also the parts of programming languages that are closest in appearance to mathematics. In the absence of side effects, program expressions have semantics that are very similar to those of mathematical expressions, which leads to semantic simplicity and precision. Unfortunately, in the presence of side effects, expressions can behave in ways that are very different from their mathematical counterparts. This can be a source of confusion and error. In fact, the semantics of expressions with side effects have a significant control component. The way that such expressions are evaluated, including the order in which subexpressions are computed, can have a major impact on their meaning, something that is never true for mathematical expressions. That is why we discuss them in this chapter, along with more explicit forms of control.

Explicit control structures first appeared in programming languages as GOTOs, which are simple imitations of the jump statements of assembly language, transferring control directly, or after a test, to a new location in the program. With Algol60 came the improvement of **structured control**, in which control statements transfer control to and from sequences of statements that are (at least in principle) **single-entry**, **single-exit**, that is, those that enter from the beginning and exit from the end. Examples of such single-entry, single-exit constructs are the **blocks** of Algol60, Algol68, C, and Ada, which may also include declarations, and which you studied in Chapter 7.¹

Structured programming led to an enormous improvement in the readability and reliability of programs. It’s no surprise, then, that structured control constructs are part of most major languages today. Some languages do away with GOTOs altogether, although a (now somewhat muted) debate continues to this day on the utility of GOTOs within the context of structured programming.

¹All these languages contain certain relaxations of the single-entry, single-exit property of these constructs, but the principle of controlling entry and exit points remains.

In this chapter, we will first discuss expressions and the variety of control questions that can arise during their evaluation. We then discuss structured control mechanisms (the assignment statement was already studied in Chapter 7), after which we review the GOTO issue. In the last section of this chapter, we begin a discussion of exception handling, which is essentially a preemptive control mechanism, causing the explicit control structure of a program to be disturbed. In that section, we discuss the appearance and operation of exceptions in several languages; implementation issues are postponed to the next chapter, since they involve the runtime environment.

### 9.1 Expressions

As you saw in Chapters 6 and 7, basic expressions are literals (manifest constants) and identifiers. More complex expressions are built up recursively from basic expressions by the application of operators and functions, sometimes involving grouping symbols such as parentheses. For example, in the simple arithmetic expression 3 + 4 * 5, the **+ operator** is applied to its two **operands**, consisting of the integer literal 3 and the (sub)expression 4 * 5, which in its turn represents the application of the * operator to its operands, consisting of the integer literals 4 and 5. Operators can take one or more operands: An operator that takes one operand is called a **unary operator**; an operator that takes two is a **binary operator**. Operators can be written in **infix**, **postfix**, or **prefix** notation, corresponding to an inorder, postorder, or preorder traversal of the syntax tree of the expression. For example, as you learned in Chapter 6, the infix expression 3 + 4 * 5 with the syntax tree shown in Figure 9.1 is written in postfix form as 3 4 5 * + and in prefix form as + 3 * 4 5.

![](img/062750ade02e28185b1fb8e8cf6dc89e_407_0.png)

Figure 9.1 Syntax tree for infix expression 3 + 4 * 5

The advantage of postfix and prefix forms is that they do not require parentheses to express the order in which operators are applied. Thus, operator precedence is not required to disambiguate an unparenthesized expression. For instance, (3 + 4) * 5 is written in postfix form as 3 4 + 5 * and in prefix form as * + 3 4 5. Associativity of operators is also expressed directly in postfix and prefix form without the need for a rule. For example, the postfix expression 3 4 5 + + right associates and 3 4 + 5 + left associates the infix expression 3 + 4 + 5.

Many languages make a distinction between operators and functions. Operators are predefined and (if binary) written in infix form, with specified associativity and precedence rules, whereas functions, which can be either predefined or user-defined, are written in prefix form and the operands are viewed as **arguments** or **actual parameters** to calls of the functions. For example, in C, if we wrote the expression 3 + 4 * 5 with user-defined addition and multiplication operations, it would appear as add(3, mul(4,5)). In fact, the distinction between operators and functions is arbitrary, since they are equivalent concepts. Historically, however, the distinction was significant, since built-in operators were implemented using highly optimized **inline code** (code for the function body that is inserted directly at

the point where the function would be called),² while function calls required the building of sometimes time-consuming **activations** (described in the next chapter). Modern translators, however, often inline even user-defined functions; in any case, the performance penalty of activations has largely disappeared in modern architectures.

Programming languages, too, have increasingly allowed programmers to overload the built-in operators and even to define new infix operators with arbitrary associativity and precedence, as you saw in Sections 3.4 and 5.4. Some languages even allow all operators to be written in either prefix or infix form. For example, 3 + 4 * 5 can be written just as well in Ada as " +"(3, "*"(4,5)). A few languages use either the prefix or postfix form exclusively, for both predefined and user-defined operations. For example, stack-based languages such as PostScript and FORTH use postfix notation exclusively, while Lisp uses prefix notation. Lisp also requires expressions to be **fully parenthesized**; that is, all operators and operands must be enclosed in parentheses. This is because LISP operators can take variable numbers of arguments as operands. Thus, 3 + 4 * 5 and (3 + 4) * 5 would look as follows in LISP:

```
(+ 3 (* 4 5))
(* (+ 3 4) 5)
```

Each programming language has rules for evaluating expressions. According to one common evaluation rule, all operands are evaluated first and then operators are applied to them. This rule, called **applicative order evaluation**, or sometimes **strict** evaluation, is the most common rule in programming languages. It corresponds to a bottom-up evaluation of the values at nodes of the syntax tree representing an expression. For example, the expression (3 + 4) * (5 − 6) is represented by the syntax tree shown in Figure 9.2.

![](img/062750ade02e28185b1fb8e8cf6dc89e_408_0.png)

Figure 9.2 Syntax tree for the expression (3 + 4) * (5 − 6)

In applicative order evaluation, first the “+” and “−” nodes are evaluated to 7 and −1, respectively, and then the “*” is applied to get −7.

Let us also consider how this would appear in terms of user-defined functions, written in prefix form in C syntax:

```
mul(add(3,4),sub(5,6))
```

Applicative order says evaluate the arguments first. Thus, calls to add (3,4) and sub(5,6) are made, which are also evaluated using applicative order. Then, the calls are replaced by their returned values, which are 7 and −1. Finally, the call

```
mul(7,-1)
```

²Code inlining is an important optimization technique for translators; indeed, C++ has an inline keyword to allow the programmer to specifically request inlining, if possible; see Chapter 6. Inlining of operators and nonrecursive functions with no nonlocal references is relatively easy, but in the most general case inlining may be difficult or impossible. For an example of the difficulties of inlining, see Exercise 11.14.
