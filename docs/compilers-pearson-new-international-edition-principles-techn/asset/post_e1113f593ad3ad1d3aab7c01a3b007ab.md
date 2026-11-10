
## 4.8 Using Ambiguous Grammars

| State | ACTION id | ACTION + | ACTION * | ACTION ( | ACTION ) | ACTION $ | GOTO E |
|---|---|---|---|---|---|---|---|
| 0 | s3 | e1 | e1 | s2 | e2 | e1 | 1 |
| 1 | e3 | s4 | s5 | e3 | e2 | acc |  |
| 2 | s3 | e1 | e1 | s2 | e2 | e1 | 6 |
| 3 | r4 | r4 | r4 | r4 | r4 | r4 |  |
| 4 | s3 | e1 | e1 | s2 | e2 | e1 | 7 |
| 5 | s3 | e1 | e1 | s2 | e2 | e1 | 8 |
| 6 | e3 | s4 | s5 | e3 | s9 | e4 |  |
| 7 | r1 | r1 | s5 | r1 | r1 | r1 |  |
| 8 | r2 | r2 | r2 | r2 | r2 | r2 |  |
| 9 | r3 | r3 | r3 | r3 | r3 | r3 |  |

Figure 4.53: LR parsing table with error routines

**e3:** Called from states 1 or 6 when expecting an operator, and an **id** or right parenthesis is found.

> push state 4 (corresponding to symbol +) onto the stack;
> issue diagnostic “missing operator.”

**e4:** Called from state 6 when the end of the input is found.

> push state 9 (for a right parenthesis) onto the stack;
> issue diagnostic “missing right parenthesis.”

On the erroneous input *id +)*, the sequence of configurations entered by the parser is shown in Fig. 4.54.

| STACK | SYMBOLS | INPUT | ACTION |
|---|---|---|---|
| 0 |  | id + ) $ |  |
| 0 3 | id | + ) $ |  |
| 0 1 | E | + ) $ |  |
| 0 1 4 | E + | ) $ | "unbalanced right parenthesis" |
| 0 1 4 | E + | $ | e2 removes right parenthesis |
| 0 1 4 | E + | $ | "missing operand" |
| 0 1 4 3 | E + id | $ | e1 pushes state 3 onto stack |
| 0 1 4 7 | E + | $ |  |
| 0 1 | E + | $ |  |

Figure 4.54: Parsing and error recovery moves made by an LR parser

### 4.8.4 Exercises for Section 4.8

**! Exercise 4.8.1:** The following is an ambiguous grammar for expressions with *n* binary, infix operators, at *n* different levels of precedence:

$$E \to E\,\theta_1\,E \mid E\,\theta_2\,E \mid \cdots \mid E\,\theta_n\,E \mid (E) \mid \mathrm{id}$$

- a) As a function of *n*, what are the SLR sets of items?
- b) How would you resolve the conflicts in the SLR items so that all operators are left associative, and $\theta_n$ takes precedence over $\theta_{n-1}$, which takes precedence over $\theta_{n-2}$, and so on?
- c) Show the SLR parsing table that results from your decisions in part (b).
- d) Repeat parts (a) and (c) for the unambiguous grammar, which defines the same set of expressions, shown in Fig. 4.55.
- e) How do the counts of the number of sets of items and the sizes of the tables for the two (ambiguous and unambiguous) grammars compare? What does that comparison tell you about the use of ambiguous expression grammars?

```
E₁ → E₁ θ₁ E₂ | E₂
E₂ → E₂ θ₂ E₃ | E₃
...
Eₙ → Eₙ θₙ Eₙ₊₁ | Eₙ₊₁
Eₙ₊₁ → ( E₁ ) | id
```

Figure 4.55: Unambiguous grammar for n operators

**! Exercise 4.8.2:** In Fig. 4.56 is a grammar for certain statements, similar to that discussed in Exercise 4.4.12. Again, *e* and *s* are terminals standing for conditional expressions and “other statements,” respectively.

![](img/2a44b9071782fade81f3050c3b718341_291_0.png)

Figure 4.56: A grammar for certain kinds of statements

- a) Build an LR parsing table for this grammar, resolving conflicts in the usual way for the dangling-else problem.
- b) Implement error correction by filling in the blank entries in the parsing table with extra reduce-actions or suitable error-recovery routines.
- c) Show the behavior of your parser on the following inputs:
  - (i) if *e* then *s* ; if *e* then *s* **end**
  - (ii) while *e* do **begin** *s* ; if *e* then *s* ; **end**

## 4.9 Parser Generators

This section shows how a parser generator can be used to facilitate the construction of the front end of a compiler. We shall use the LALR parser generator Yacc as the basis of our discussion, since it implements many of the concepts discussed in the previous two sections and it is widely available. Yacc stands for “yet another compiler-compiler,” reflecting the popularity of parser generators in the early 1970s when the first version of Yacc was created by S. C. Johnson. Yacc is available as a command on the UNIX system, and has been used to help implement many production compilers.

### 4.9.1 The Parser Generator Yacc

A translator can be constructed using Yacc in the manner illustrated in Fig. 4.57. First, a file, say translate.y, containing a Yacc specification of the translator is prepared. The UNIX system command

```
yacc translate.y
```

transforms the file translate.y into a C program called y.tab.c using the LALR method outlined in Algorithm 4.63. The program y.tab.c is a representation of an LALR parser written in C, along with other C routines that the user may have prepared. The LALR parsing table is compacted as described in Section 4.7. By compiling y.tab.c along with the ly library that contains the LR parsing program using the

```
cc y.tab.c -ly
```

we obtain the desired object program a.out that performs the translation specified by the original Yacc program.⁷ If other procedures are needed, they can be compiled or loaded with y.tab.c, just as with any C program.

⁷ The name ly is system dependent.

![](img/2a44b9071782fade81f3050c3b718341_292_0.png)

Figure 4.57: Creating an input/output translator with Yacc

A Yacc source program has three parts:

```
declarations
%%
translation rules
%%
supporting C routines
```

**Example 4.69:** To illustrate how to prepare a Yacc source program, let us construct a simple desk calculator that reads an arithmetic expression, evaluates it, and then prints its numeric value. We shall build the desk calculator starting with the following grammar for arithmetic expressions:

```
E → E + T | T
T → T * F | F
F → ( E ) | digit
```

The token `digit` is a single digit between 0 and 9. A Yacc desk calculator program derived from this grammar is shown in Fig. 4.58. □

```
%{
#include <ctype.h>
%}

%token DIGIT

%%
line   : expr '\n'      { printf("%d\n", $1); }
       ;
expr   : expr '+' term  { $$ = $1 + $3; }
       | term
       ;
term   : term '*' factor { $$ = $1 * $3; }
       | factor
       ;
factor : '(' expr ')'  { $$ = $2; }
       | DIGIT
       ;

%%
yylex() {
    int c;
    c = getchar();
    if (isdigit(c)) {
        yylval = c-'0';
        return DIGIT;
    }
    return c;
}
```

Figure 4.58: Yacc specification of a simple desk calculator

### The Declarations Part

There are two sections in the declarations part of a Yacc program; both are optional. In the first section, we put ordinary C declarations, delimited by `%{` and `%}`. Here we place declarations of any temporaries used by the translation rules or procedures of the second and third sections. In Fig. 4.58, this section contains only the include-statement

```c
#include <ctype.h>
```

that causes the C preprocessor to include the standard header file `<ctype.h>` that contains the predicate `isdigit`.
Also in the declarations part are declarations of grammar tokens. In Fig. 4.58, the statement

```yacc
%token DIGIT
```

declares DIGIT to be a token. Tokens declared in this section can then be used in the second and third parts of the Yacc specification. If Lex is used to create the lexical analyzer that passes tokens to the Yacc parser, then these token declarations are also made available to the analyzer generated by Lex, as discussed in Section 3.5.2.

### The Translation Rules Part

In the part of the Yacc specification after the first %% pair, we put the translation rules. Each rule consists of a grammar production and the associated semantic action. A set of productions that we have been writing:

⟨head⟩ → ⟨body⟩₁ | ⟨body⟩₂ | … | ⟨body⟩ₙ

would be written in Yacc as

```
⟨head⟩ : ⟨body⟩₁   {semantic action}₁
       | ⟨body⟩₂   {semantic action}₂
       ...
       | ⟨body⟩ₙ   {semantic action}ₙ
       ;
```

In a Yacc production, unquoted strings of letters and digits not declared to be tokens are taken to be nonterminals. A quoted single character, e.g. `'c'`, is taken to be the terminal symbol c, as well as the integer code for the token represented by that character (i.e., Lex would return the character code for `'c'` to the parser, as an integer). Alternative bodies can be separated by a vertical bar, and a semicolon follows each head with its alternatives and their semantic actions. The first head is taken to be the start symbol.

A Yacc semantic action is a sequence of C statements. In a semantic action, the symbol `$$` refers to the attribute value associated with the nonterminal of the head, while `$i` refers to the value associated with the ith grammar symbol (terminal or nonterminal) of the body. The semantic action is performed whenever we reduce by the associated production, so normally the semantic action computes a value for `$$` in terms of the `$i`’s. In the Yacc specification, we have written the two E-productions

```
E → E + T  |  T
```

and their associated semantic actions as:

```
expr : expr '+' term   { $$ = $1 + $3; }
     | term
     ;
```

Note that the nonterminal term in the first production is the third grammar symbol of the body, while + is the second. The semantic action associated with the first production adds the value of the expr and the term of the body and assigns the result as the value for the nonterminal expr of the head. We have omitted the semantic action for the second production altogether, since copying the value is the default action for productions with a single grammar symbol in the body. In general, `{ $$ = $1; }` is the default semantic action. Notice that we have added a new starting production

```
line : expr '\n'      { printf("%d\n", $1); }
```

to the Yacc specification. This production says that an input to the desk calculator is to be an expression followed by a newline character. The semantic action associated with this production prints the decimal value of the expression followed by a newline character.
