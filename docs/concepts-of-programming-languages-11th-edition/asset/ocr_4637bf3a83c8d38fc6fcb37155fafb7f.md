and indirect left recursion from a grammar. The other problem is detected with the pairwise disjointness test, which tests whether a parsing subprogram can determine which RHS is being parsed on the basis of the next token of input. Some grammars that fail the pairwise disjointness test often can be modified to pass it, using left factoring.

The parsing problem for bottom-up parsers is to find the substring of the current sentential form that must be reduced to its associated LHS to get the next (previous) sentential form in the rightmost derivation. This substring is called the handle of the sentential form. A parse tree can provide an intuitive basis for recognizing a handle. A bottom-up parser is a shift-reduce algorithm, because in most cases it either shifts the next lexeme of input onto the parse stack or reduces the handle that is on top of the stack.

The LR family of shift-reduce parsers is the most commonly used bottom-up parsing approach for programming languages, because parsers in this family have several advantages over alternatives. An LR parser uses a parse stack, which contains grammar symbols and state symbols to maintain the state of the parser. The top symbol on the parse stack is always a state symbol that represents all of the information in the parse stack that is relevant to the parsing process. LR parsers use two parsing tables: ACTION and GOTO. The ACTION part specifies what the parser should do, given the state symbol on top of the parse stack and the next token of input. The GOTO table is used to determine which state symbol should be placed on the parse stack after a reduction has been done.

# ## REVIEW QUESTIONS

+   1. What are three reasons why syntax analyzers are based on grammars?
+   2. Explain the three reasons why lexical analysis is separated from syntax analysis.
+   3. Define *lexeme* and *token*.
+   4. What are the primary tasks of a lexical analyzer?
+   5. Describe briefly the three approaches to building a lexical analyzer.
+   6. What is a state transition diagram?
+   7. Why are character classes used, rather than individual characters, for the letter and digit transitions of a state diagram for a lexical analyzer?
+   8. What are the two distinct goals of syntax analysis?
+   9. Describe the differences between top-down and bottom-up parsers.
+   10. Describe the parsing problem for a top-down parser.
+   11. Describe the parsing problem for a bottom-up parser.
+   12. Explain why compilers use parsing algorithms that work on only a subset of all grammars.
+   13. Why are named constants used, rather than numbers, for token codes?