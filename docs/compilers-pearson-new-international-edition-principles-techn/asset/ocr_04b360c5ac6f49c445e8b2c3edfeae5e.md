# 3.1.  THE ROLE OF THE LEXICAL ANALYZER

+   1. Simplicity of design is the most important consideration. The separation of lexical and syntactic analysis often allows us to simplify at least one of these tasks. For example, a parser that had to deal with comments and whitespace as syntactic units would be considerably more complex than one that can assume comments and whitespace have already been removed by the lexical analyzer. If we are designing a new language, separating lexical and syntactic concerns can lead to a cleaner overall language design.
+   
+   2. Compiler efficiency is improved. A separate lexical analyzer allows us to apply specialized techniques that serve only the lexical task, not the job of parsing. In addition, specialized buffering techniques for reading input characters can speed up the compiler significantly.
+   
+   3. Compiler portability is enhanced. Input-device-specific peculiarities can be restricted to the lexical analyzer.

# 3.1.2  Tokens, Patterns, and Lexemes

When discussing lexical analysis, we use three related but distinct terms:

+   - *A token* is a pair consisting of a token name and an optional attribute value. The token name is an abstract symbol representing a kind of lexical unit, e.g., a particular keyword, or a sequence of input characters denoting an identifier. The token names are the input symbols that the parser processes. In what follows, we shall generally write the name of a token in boldface. We will often refer to a token by its token name.
+   
+   - *A pattern* is a description of the form that the lexemes of a token may take. In the case of a keyword as a token, the pattern is just the sequence of characters that form the keyword. For identifiers and some other tokens, the pattern is a more complex structure that is *matched* by many strings.
+   
+   - *A lexeme* is a sequence of characters in the source program that matches the pattern for a token and is identified by the lexical analyzer as an instance of that token.

**Example 3.1:** Figure 3.2 gives some typical tokens, their informally described patterns, and some sample lexemes. To see how these concepts are used in practice, in the C statement

```
```c
printf("Total = %d\n", score);
```
```

both printf and score are lexemes matching the pattern for token id, and "Total = %d\n" is a lexeme matching literal.

In many programming languages, the following classes cover most or all of the tokens: