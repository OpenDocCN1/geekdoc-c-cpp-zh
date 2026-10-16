Right-recursive rules on the other hand, as we have already noted, present no such problem in recursive-descent parsing. However, the code that we write for a right-recursive rule such as:

expr → term @ expr | term

(we change the name of the operation to @ to avoid confusion with +) also corresponds to the use of square brackets in EBNF to express this optional structure:

expr → term [ @ expr ]

This process is called left factoring, since it is as if the term in both alternatives of the grammar rule is “factored out,” leaving either @ expr or nothing (thus making @ expr optional).

Another typical left-factoring situation arises when we have an if-statement with an optional else-part:

if-statement → if ( expression ) statement | if ( expression ) statement else statement

This cannot be translated directly into code, since both alternatives begin with the same prefix. As in the previous example, in EBNF this is written with square brackets, and the common parts of the alternatives are “factored out”:

if-statement → if ( expression ) statement [ else statement ]

This corresponds directly to the recursive-descent code to parse an if-statement:

```
void ifStatement(){
    match("if", "if expected");
    match("(", "( expected");
    expression();
    match(")", ") expected");
    statement();
    if (token == "else"){
        match("else", "else expected");
        statement();
    }
}
```

Thus, in both left-recursive and left-factoring situations, EBNF rules or syntax diagrams correspond naturally to the code of a recursive-descent parser. This actually is one of the main reasons for their use.

As a demonstration of the power and ease of recursive-descent parsing, Figure 6.24 provides the complete code in C for an integer calculator based on the grammar of Figure 6.18. This program accepts a single line of input containing a simple integer arithmetic expression consisting of numbers, the operators + and *, and parentheses, and prints the computed value of the expression, or an error message if the expression is not syntactically correct. As in the grammar, the calculator assumes all tokens are characters, and it does not permit spaces to appear in an expression. To make it easy to print the computed value, and also to make sure only a single expression is entered in the input line,