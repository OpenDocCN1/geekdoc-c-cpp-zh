+   Outline
+   5.1 Introduction
+   5.2 Control Structures
+   5.2.1 Sequence Structure
+   5.2.2 Selection Statements
+   5.2.3 Iteration Statements
+   5.2.4 Summary of Control Statements
+   5.3 if Single-Selection Statement
+   5.4 if...else Double-Selection Statement
+   5.4.1 Nested if...else Statements
+   5.4.2 Dangling-else Problem
+   5.4.3 Blocks
+   5.4.4 Conditional Operator (?:)
+   5.5 Student Class: Nested if...else Statements
+   5.6 while Iteration Statement
+   5.7 Counter-Controlled Iteration
+   5.7.1 Implementing Counter-Controlled Iteration
+   5.7.2 Integer Division and Truncation
+   5.8 Sentinel-Controlled Iteration
+   5.8.1 Implementing Sentinel-Controlled Iteration
+   5.8.2 Program Logic for Sentinel-Controlled Iteration
+   5.8.5 Braces in a while Statement
+   5.8.4 Converting Between Simple Types Explicitly and Implicitly
+   5.8.5 Formatting Floating-Point Numbers
+   5.9 Nested Control Statements
+   5.10 Compound Assignment Operators
+   5.11 Increment and Decrement Operators
+   5.11.1 Prefix Increment vs. Postfix Increment
+   5.11.2 Simplifying Increment Statements
+   5.11.3 Operator Precedence and Associativity
+   5.12 Simple Types
+   5.13 Wrap-Up

# 5.1 Introduction

In this chapter, we discuss C#’s if statement in additional detail and introduce the if...else and while statements—all of these building blocks allow you to specify the logic required for methods and properties to perform their tasks. We also introduce the compound assignment operators and the increment and decrement operators. Finally, we discuss additional details of C#’s simple types.

# 5.2 Control Structures

Normally, statements execute one after the other in the order in which they’re written. This process is called sequential execution. Various C# statements enable you to specify that the next statement to execute is not necessarily the next one in sequence. This is called transfer of control.

During the 1960s, it became clear that the indiscriminate use of transfers of control was the root of much difficulty experienced by software development groups. The blame was pointed at the goto statement (used in most programming languages of the time), which allows you to specify a transfer of control to one of a wide range of destinations in a program.

The research of Bohm and Jacopini had demonstrated that programs could be written without any goto statements. The challenge for programmers of the era was to shift