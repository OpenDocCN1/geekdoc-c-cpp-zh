# Parentheses

Use more parentheses than you think you need. Use parentheses to clarify expressions that involve more than two terms. They may not be needed, but they add clarity and they don’t cost you anything. For example, how are the following expressions evaluated?

C++ version: 12 + 4 % 3 * 7 / 8

Microsoft Visual Basic version: 12 + 4 mod 3 * 7 / 8

The key question is, did you have to think about how the expressions are evaluated? Can you be confident in your answer without checking some references? Even experienced programmers don’t answer confidently, and that’s why you should use parentheses whenever there’s any doubt about how an expression is evaluated.

# 31.3 Layout Styles

Most layout issues have to do with laying out blocks, the groups of statements below control statements. A block is enclosed between braces or keywords: { and } in C++ and Java, if-then-endif in Visual Basic, and other similar structures in other languages. For simplicity, much of this discussion uses begin and end generically, assuming that you can figure out how the discussion applies to braces in C++ and Java or other blocking mechanisms in other languages. The following sections describe four general styles of layout:

+   - Pure blocks
+   - Emulating pure blocks
+   - Using begin-end pairs (braces) to designate block boundaries
+   - Endline layout

# Pure Blocks

Much of the layout controversy stems from the inherent awkwardness of the more popular programming languages. A well-designed language has clear block structures that lend themselves to a natural indentation style. In Visual Basic, for example, each control construct has its own terminator and you can’t use a control construct without using the terminator. Code is blocked naturally. Some examples in Visual Basic are shown in Listing 31-6, Listing 31-7, and Listing 31-8: