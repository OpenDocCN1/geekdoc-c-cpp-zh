
This situation occurs so frequently that a special notation for such grammar rules is adopted that expresses more clearly the repetitive nature of their structures:

```
number → digit {digit}
```

and:

```
expr → term { + term }
```

In this notation, the curly brackets { } stand for “zero or more repetitions of.” Thus, the rules express that a number is a sequence of one or more digits, and an expression is a term followed by zero or more repetitions of a + and another term. In this notation, the curly brackets have become new metasymbols, and this notation is called extended Backus-Naur form, or EBNF for short.

This new notation obscures the left associativity of the + operator that is expressed by the left recursion in the original rule in BNF. We can get around this by simply assuming that any operator involved in a curly bracket repetition is left-associative. Indeed, if an operator were right-associative, the corresponding grammar rule would be right-recursive. Right-recursive rules are usually not written using curly brackets (the reason for this is explained more fully in the next section). The problem of expressing right associativity points out a flaw in EBNF grammars: Parse trees and syntax trees cannot be written directly from the grammar. Therefore, we will always use BNF notation to write parse trees.

A second common situation is for a structure to have an optional part, such as the optional else-part of an if-statement in C, which is expressed in BNF notation for C as follows:

```
if-statement → if ( expression ) statement |
                if ( expression ) statement else statement
```

This is written more simply and expressively in EBNF, as follows:

```
if-statement → if ( expression ) statement [ else statement ]
```

where the square brackets “[ ]” are new metasymbols indicating optional parts of the structure.

Another example is the grammar rule for function-definition in the BNF grammar for C; see Figure 6.6:

```
function-definition → declaration-specifiers declarator
                     declaration-list compound-statement
                     | declaration-specifiers declarator compound-statement
                     | declarator declaration-list compound-statement
                     | declarator compound-statement
```

Using EBNF, this can be much more simply expressed as:

```
function-definition → [ declaration-specifiers ] declarator
                     [ declaration-list ] compound-statement
```

Right-associative (binary) operators can also be written using these new metasymbols. For example, if “@” is a right-associative operator with BNF:

```
expr → term @ expr | term
```

then this rule can be rewritten in EBNF as follows:

```
expr → term [ @ expr ]
```

For completeness, we write out the grammar of Figure 6.3 for simple integer arithmetic expressions in EBNF in Figure 6.18.

```
expr → term { + term }
term → factor { * factor }
factor → ( expr ) | number
number → digit { digit }
digit → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

Figure 6.18 EBNF rules for simple integer arithmetic expressions

A sometimes-useful graphical representation for a grammar rule is the syntax diagram, which indicates the sequence of terminals and nonterminals encountered in the right-hand side of the rule. For example, syntax diagrams for noun-phrase and article of our simple English grammar presented in Section 6.2 would be drawn as shown in Figure 6.19. Figure 6.20 shows these two rules condensed into one.

![](img/062750ade02e28185b1fb8e8cf6dc89e_228_0.png)

![](img/062750ade02e28185b1fb8e8cf6dc89e_228_1.png)

Figure 6.19: Syntax diagrams for noun-phrase and article of the simple English grammar presented in Section 6.2

![](img/062750ade02e28185b1fb8e8cf6dc89e_228_2.png)

Figure 6.20: Condensed version of diagrams shown in Figure 6.19

Syntax diagrams use circles or ovals for terminals and squares or rectangles for nonterminals, connecting them with lines and arrows to indicate appropriate sequencing. Syntax diagrams can also condense several grammar rules into one diagram.

Syntax diagrams for the expression grammar in Figure 6.18 are given in Figure 6.21. Note the use of loops in the diagrams to express the repetition given by the curly brackets in the EBNFs.

![](img/062750ade02e28185b1fb8e8cf6dc89e_230_0.png)

Figure 6.22 Syntax diagram for the if-statement in C

Syntax diagrams are always written from the EBNF notation, not the BNF notation, for reasons that are made clear in the next section. Thus, the diagram for expr shown in Figure 6.23 would be incorrect.

![](img/062750ade02e28185b1fb8e8cf6dc89e_230_1.png)

Figure 6.23: Incorrect syntax diagram for expr

Syntax diagrams are visually appealing but take up a great deal of space. As more programmers have become familiar with rules written directly in BNF or EBNF, syntax diagrams have been used less frequently, and now are seen much more rarely than in the past. They remain useful, however, as flow charts for writing parsing procedures, a topic to which we now turn.

# 6.6 Parsing Techniques and Tools

A grammar written in BNF, EBNF, or as syntax diagrams describes the strings of tokens that are syntactically legal in a programming language. The grammar, thus, also implicitly describes the actions that a parser must take to parse a string of tokens correctly and to construct, either implicitly or explicitly, a derivation or parse tree for the string. The simplest form of a parser is a recognizer—a program that accepts or rejects strings, based on whether they are legal strings in the language. More general parsers build parse trees (or, more likely, abstract syntax trees) and carry out other operations, such as calculating values for expressions.

Given a grammar in one of the forms we have discussed, how does it correspond to the actions of a parser? One method of parsing attempts to match an input with the right-hand sides of the grammar rules. When a match occurs, the right-hand side is replaced by, or reduced to, the nonterminal on the left. Such parsers are bottom-up parsers, since they construct derivations and parse trees from the leaves to the root. They are sometimes also called shift-reduce parsers, since they shift tokens onto a stack prior to reducing strings to nonterminals. In the other major parsing method, top-down parsing, nonterminals are expanded to match incoming tokens and directly construct a derivation. Both top-down and bottom-up parsing can be automated; that is, a program, called a parser generator, can be written that will automatically translate a BNF description into a parser. Since bottom-up parsing is somewhat more powerful than top-down parsing, it is usually the preferred method for parser generators (also called compiler compilers). One such parser generator in wide use is YACC (short for “yet another compiler compiler”), or its freeware version Bison, which we will study later in this section.

However, is an older, very effective method for constructing a parser from a grammar that is still in use. This method, which is called recursive-descent parsing, turns the nonterminals into a group of mutually recursive procedures whose actions are based on the right-hand sides of the BNFs.

The right-hand sides are interpreted in the procedures as follows: tokens are matched directly with input tokens as constructed by a scanner. Nonterminals are interpreted as calls to the procedures corresponding to the nonterminals.

As an example, in our simplified English grammar, procedures for sentence, noun-phrase, and article would be written as follows (in C-like pseudocode):

```
void sentence(){
    nounPhrase();
    verbPhrase();
}

void nounPhrase(){
    article();
    noun();
}

void article(){
    if (token == "a") match("a", "a expected");
    else if (token == "the") match("the", "the expected");
    else error("article expected");
}
```

In this pseudocode, we use strings to imitate tokens, and a global variable called token to hold the current token as constructed by a scanner. The getToken procedure of the scanner is called whenever a new token is desired. A match of a token corresponds to a successful test for that token, followed by a call to getToken:

```
void match(TokenType expected, char* message){
    if (token == expected) getToken();
    else error(message);
}
```

Each parsing procedure starts with the variable token already holding the first token that should be expected. Thus, a call to getToken must precede the first call to the sentence procedure. Likewise, each parsing procedure leaves behind the next token in the input stream when it is finished. The error procedure prints an error message and aborts the parse. (Note that errors need only be detected when actual tokens are expected, as in the procedure article. We could have checked for “a” or “the” in the sentence procedure, but in this scheme it is unnecessary.)

If we apply this process to the BNF description of Figure 6.17, we encounter a problem with the left-recursive rules such as the one for an expression:

expr → expr + term | term
