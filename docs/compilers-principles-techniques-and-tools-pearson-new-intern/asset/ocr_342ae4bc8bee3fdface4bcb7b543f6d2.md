# 2.6.  *LEXICAL ANALYSIS*

shall take this opportunity to allow multiplication and division as well. The extended translation scheme appears in Fig. 2.28.

```
expr  →  expr + term    { print('+') }
      |  expr - term    { print('-') }
      |  term

term  →  term * factor  { print('*') }
      |  term / factor  { print('/') }
      |  factor

factor → ( expr )
       | num            { print(num.value) }
       | id             { print(id.lexeme) }
```

Figure 2.28: Actions for translating into postfix notation

In Fig. 2.28, the terminal **num** is assumed to have an attribute *num.value*, which gives the integer value corresponding to this occurrence of **num**. Terminal **id** has a string-valued attribute written as *id.lexeme*; we assume this string is the actual lexeme comprising this instance of the token **id**.

The pseudocode fragments used to illustrate the workings of a lexical analyzer will be assembled into Java code at the end of this section. The approach in this section is suitable for hand-written lexical analyzers. Section 3.5 describes a tool called Lex that generates a lexical analyzer from a specification. Symbol tables or data structures for holding information about identifiers are considered in Section 2.7.

# 2.6.1  Removal of White Space and Comments

The expression translator in Section 2.5 sees every character in the input, so extraneous characters, such as blanks, will cause it to fail. Most languages allow arbitrary amounts of white space to appear between tokens. Comments are likewise ignored during parsing, so they may also be treated as white space.

If white space is eliminated by the lexical analyzer, the parser will never have to consider it. The alternative of modifying the grammar to incorporate white space into the syntax is not nearly as easy to implement.

The pseudocode in Fig. 2.29 skips white space by reading input characters as long as it sees a blank, a tab, or a newline. Variable *peek* holds the next input character. Line numbers and context are useful within error messages to help pinpoint errors; the code uses variable *line* to count newline characters in the input.