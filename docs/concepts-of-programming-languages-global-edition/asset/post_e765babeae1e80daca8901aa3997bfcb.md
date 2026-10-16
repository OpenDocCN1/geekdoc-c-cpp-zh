
# Figure 4.4

The structure of an LR parser

![](img/e382387aad0004c80a0dd0a70be9a623_211_0.png)

Notice that the input string has a dollar sign at its right end. This sign is put there during initialization of the parser. It is used for normal termination of the parser. Using this parser configuration, we can formally define the LR parser process, which is based on the parsing table.

An LR parsing table has two parts, named ACTION and GOTO. The ACTION part of the table specifies most of what the parser does. It has state symbols as its row labels and the terminal symbols of the grammar as its column labels. Given a current parser state, which is represented by the state symbol on top of the parse stack, and the next symbol (token) of input, the parse table specifies what the parser should do. The two primary parser actions are shift and reduce. Either the parser shifts the next input symbol onto the parse stack or it already has the handle on top of the stack, which it reduces to the LHS of the rule whose RHS is the same as the handle. Two other actions are possible: accept, which means the parser has successfully completed the parse of the input, and error, which means the parser has detected a syntax error.

The rows of the GOTO part of the LR parsing table have state symbols as labels. This part of the table has nonterminals as column labels. The values in the GOTO part of the table indicate which state symbol should be pushed onto the parse stack after a reduction has been completed, which means the handle has been removed from the parse stack and the new nonterminal has been pushed onto the parse stack. The specific symbol is found at the row whose label is the state symbol on top of the parse stack after the handle and its associated state symbols have been removed. The column of the GOTO table that is used is the one with the label, that is the LHS of the rule used in the reduction.

Consider the traditional grammar for arithmetic expressions that follows:

- 1. E → E + T
- 2. E → T
- 3. T → T * F
- 4. T → F
- 5. F → (E)
- 6. F → id

The rules of this grammar are numbered to provide a simple way to reference them in a parsing table.

# Figure 4.5

The LR parsing table for an arithmetic expression grammar

Abbreviations are used for the actions: R for reduce and S for shift. R4 means reduce using rule 4; S6 means shift the next symbol of input onto the stack and push state S6 onto the stack. Empty positions in the ACTION table indicate syntax errors. In a complete parser, these could have calls to error-handling routines.

LR parsing tables can easily be constructed using a software tool, such as yacc (Johnson, 1975), which takes the grammar as input. Although LR parsing tables can be produced by hand, for a grammar of a real programming language, the task would be lengthy, tedious, and error prone. For real compilers, LR parsing tables are always generated with software tools.

The initial configuration of an LR parser is

(S0, a1 ... an$)

The parser actions are informally defined as follows:

- 1. The Shift process is simple: The next symbol of input is pushed onto the stack, along with the state symbol that is part of the Shift specification in the ACTION table.
- 2. For a Reduce action, the handle must be removed from the stack. Because for every grammar symbol on the stack there is a state symbol, the number of symbols removed from the stack is twice the number

# Figure 4.5

The LR parsing table for an arithmetic expression grammar

|  | Action |  |  |  |  |  | Goto |  |  |
|---|---|---|---|---|---|---|---|---|---|
| State | id | + | * | ( | ) | $ | E | T | F |
| 0 | S5 |  |  | S4 |  |  | 1 | 2 | 3 |
| 1 |  | S6 |  |  |  | accept |  |  |  |
| 2 |  | R2 | S7 |  | R2 | R2 |  |  |  |
| 3 |  | R4 | R4 |  | R4 | R4 |  |  |  |
| 4 | S5 |  |  | S4 |  |  | 8 | 2 | 3 |
| 5 |  | R6 | R6 |  | R6 | R6 |  |  |  |
| 6 | S5 |  |  | S4 |  |  |  | 9 | 3 |
| 7 | S5 |  |  | S4 |  |  |  |  | 10 |
| 8 |  | S6 |  |  | S11 |  |  |  |  |
| 9 |  | R1 | S7 |  | R1 | R1 |  |  |  |
| 10 |  | R3 | R3 |  | R3 | R3 |  |  |  |
| 11 |  | R5 | R5 |  | R5 | R5 |  |  |  |

of symbols in the handle. After removing the handle and its associated state symbols, the LHS of the rule is pushed onto the stack. Finally, the GOTO table is used, with the row label being the symbol that was exposed when the handle and its state symbols were removed from the stack, and the column label being the nonterminal that is the LHS of the rule used in the reduction.

3. When the action is Accept, the parse is complete and no errors were found.

4. When the action is Error, the parser calls an error-handling routine.

Although there are many parsing algorithms based on the LR concept, they differ only in the construction of the parsing table. All LR parsers use this same parsing algorithm.

Perhaps the best way to become familiar with the LR parsing process is through an example. Initially, the parse stack has the single symbol 0, the parser. The input stack contains the input string with an end marker, in this case a dollar sign, attached to its right end. At each step, the parser actions are dictated by the top (rightmost in Figure 4.4) symbol of the parse stack and the next (leftmost in Figure 4.4) symbol of the input. The correct action is chosen from the corresponding cell of the ACTION part of the parse table. The GOTO part of the parse table is used after a reduction action. Recall that GOTO is used to determine which state symbol is placed on the parse stack after a reduction.

Following is a trace of a parse of the string id + id * id, using the LR parsing algorithm and the parsing table shown in Figure 4.5.

| Stack | Input | Action |
|-------|-------|--------|
| 0 | id + id $ | Shift 5 |
| 0id5 | + id * $ | Reduce 6 (use GOTO[0, F]) |
| 0F3 | + id * $ | Reduce 4 (use GOTO[0, T]) |
| 0T2 | + id * $ | Reduce 2 (use GOTO[0, E]) |
| 0E1 | + id * $ | Shift 6 |
| 0E1+6 | id * $ | Shift 5 |
| 0E1+6id5 | * id $ | Reduce 6 (use GOTO[6, F]) |
| 0E1+6F3 | * id $ | Reduce 4 (use GOTO[6, T]) |
| 0E1+6T9 | * id $ | Shift 7 |
| 0E1+6T9*7 | id $ | Shift 5 |
| 0E1+6T9*7id5 | $ | Reduce 6 (use GOTO[7, F]) |
| 0E1+6T9*7F10 | $ | Reduce 3 (use GOTO[6, T]) |
| 0E1+6T9 | $ | Reduce 1 (use GOTO[0, E]) |
| 0E1 | $ | Accept |

The algorithms to generate LR parsing tables from given grammars, which are described in Aho et al. (2006), are not overly complex but are beyond the scope of a book on programming languages. As stated previously, there are a number of different software systems available to generate LR parsing tables.

# SUMMARY

Syntax analysis is a common part of language implementation, regardless of the implementation approach used. Syntax analysis is normally based on a formal syntax description of the language being implemented. A context-free grammar, which is also called BNF, is the most common approach for describing syntax. The task of syntax analysis is usually divided into two parts: lexical analysis and syntax analysis. There are several reasons for separating lexical analysis—namely, simplicity, efficiency, and portability.

A lexical analyzer is a pattern matcher that isolates the small-scale parts of a program, which are called lexemes. Lexemes occur in categories, such as integer literals and names. These categories are called tokens. Each token is assigned a numeric code, which along with the lexeme is what the lexical analyzer produces. There are three distinct approaches to constructing a lexical analyzer: using a software tool to generate a table for a table-driven analyzer, building such a table by hand, and writing code to implement a state diagram description of the tokens of the language being implemented. The state diagram for tokens can be reasonably small if character classes are used for transitions, rather than having transitions for every possible character from every state node. Also, the state diagram can be simplified by using a table lookup to recognize reserved words.

Syntax analyzers have two goals: to detect syntax errors in a given program and to produce a parse tree, or possibly only the information required to build such a tree, for a given program. Syntax analyzers are either top-down, meaning they construct leftmost derivations and a parse tree in top-down order, or bottom-up, in which case they construct the reverse of a rightmost derivation and a parse tree in bottom-up order. Parsers that work for all unambiguous grammars have complexity O(n³). However, parsers used for implementing syntax analyzers for programming languages work on subclasses of unambiguous grammars and have complexity O(n).

A recursive-descent parser is an LL parser that is implemented by writing code directly from the grammar of the source language. EBNF is ideal as the basis for recursive-descent parsers. A recursive-descent parser has a subprogram for each nonterminal in the grammar. The code for a given grammar rule is simple if the rule has a single RHS. The RHS is examined left to right. For each nonterminal, the code calls the associated subprogram for that nonterminal, which parses whatever the nonterminal generates. For each terminal, the code compares the terminal with the next token of input. If they match, the code simply calls the lexical analyzer to get the next token. If they do not, the subprogram reports a syntax error. If a rule has more than one RHS, the subprogram must first determine which RHS it should parse. It must be possible to make this determination on the basis of the next token of input.

Two distinct grammar characteristics prevent the construction of a recursive-descent parser based on the grammar. One of these is left recursion. The process of eliminating direct left recursion from a grammar is relatively simple. Although we do not cover it, an algorithm exists to remove both direct
