The **lexical structure** of a programming language is the structure of the language’s words, which are usually called **tokens**. Thus, lexical structure is similar to spelling in a natural language. In the example of a C **if** statement, the words **if** and **else** are tokens. Other tokens in programming languages include identifiers (or names), symbols for operations, such as + and * and special punctuation symbols such as the semicolon (;) and the period (.).

In this book, we shall consider syntax and lexical structure together; a more detailed study can be found in Chapter 6.

# 1.4.2 Language Semantics

Syntax represents only the surface structure of a language and, thus, is only a small part of a language definition. The semantics, or meaning, of a language is much more complex and difficult to describe precisely. The first difficulty is that “meaning” can be defined in many different ways. Typically, describing the meaning of a piece of code involves describing the effects of executing the code, but there is no standard way to do this. Moreover, the meaning of a particular mechanism may involve interactions with other mechanisms in the language, so that a comprehensive description of its meaning in all contexts may become extremely complex.

To continue with our example of the C **if** statement, its semantics may be described in words as follows (adapted from Kernighan and Richie [1988]):

> An **if** statement is executed by first evaluating its expression, which must have an arithmetic or pointer type, including all side effects, and if it compares unequal to 0, the statement following the expression is executed. If there is an **else** part, and the expression is 0, the statement following the “else” is executed.

This description itself points out some of the difficulty in specifying semantics, even for a simple mechanism such as the **if** statement. The description makes no mention of what happens if the condition evaluates to 0, but there is no else part (presumably nothing happens; that is, the program continues at the point after the **if** statement). Another important question is whether the **if** statement is “safe” in the sense that there are no other language mechanisms that may permit the statements inside an **if** statement to be executed without the corresponding evaluation of the **if** expression. If so, then the if-statement provides adequate protection from errors during execution, such as division by zero:

```
if (x != 0) y = 1 / x;
```

Otherwise, additional protection mechanisms may be necessary (or at least the programmer must be aware of the possibility of circumventing the if expression).

The alternative to this informal description of semantics is to use a formal method. However, no generally accepted method, analogous to the use of context-free grammars for syntax, exists here either. Indeed, it is still not customary for a formal definition of the semantics of a programming language to be given at all. Nevertheless, several notational systems for formal definitions have been developed and are increasingly in use. These include **operational semantics**, **denotational semantics**, and **axiomatic semantics**.

Language semantics are implicit in many of the chapters of this book, but semantic issues are more specifically addressed in Chapters 7 and 11. Chapter 12 discusses formal methods of semantic definition, including operational, denotational, and axiomatic semantics.