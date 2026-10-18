Finally, the | symbol denotes a logical alternative between the productions. Hence, D → 0 | 1 means either 0 or 1 fulfills the D production, and so on.

These grammar rules reflect operator precedence and associativity. The process of fitting grammar rules to an expression is called *parsing*. An example of parsing one of the previous expressions with the previous grammar rules is shown in Figure 6.12.

Parsing is preceded by a *lexical analysis* that splits an expression into meaningful language categories such as numbers and operators called *tokens*. There are special programs, such as *lex* and *flex*, that do the job. But the good news is that for most simple grammars, any regular expression engine, such as the C++ *regex* library discussed in Section 6.2.1, can be used if provided with proper pattern definitions.

We are ready to implement a program that performs the lexical analysis and parsing in accordance with the previous grammar rules. In the first attempt, we may consider implementing nonterminal symbols as functions. On the other hand, the terminal symbols can be directly matched from

![](bbox=[0.333, 0.359, 0.674, 0.849])

**Figure 6.12**  Parsing the expression 3+(4/5-6). An expression is syntax-compliant if the entire expression can be completely derived from the grammar rules. Otherwise there is a syntax error. The grammar reflects operator precedence and associativity. Parsing is preceded by lexical analysis, which splits an expression into meaningful language categories such as numbers and operators.