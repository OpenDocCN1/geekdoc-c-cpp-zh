
production in the lexical grammar. Each successive indented line contains a possible expansion of the non-terminal given as a sequence of non-terminal or terminal symbols. [Example: The production:

```
while-statement:
    while ( boolean-expression ) embedded-statement
```

defines a while-statement to consist of the token while, followed by the token “(”, followed by a boolean-expression, followed by the token “)”, followed by an embedded-statement. end example]

When there is more than one possible expansion of a non-terminal symbol, the alternatives are listed on separate lines. [Example: The production:

```
statement-list:
    statement
    statement-list statement
```

defines a statement-list to either consist of a statement or consist of a statement-list followed by a statement. In other words, the definition is recursive and specifies that a statement list consists of one or more statements. end example]

A subscripted suffix "opt" is used to indicate an optional symbol. [Example: The production:

```
block:
    { statement-list_opt }
```

is shorthand for:

```
block:
    { }
    { statement-list }
```

and defines a block to consist of an optional statement-list enclosed in “{” and “}” tokens. end example]

Alternatives are normally listed on separate lines, though in cases where there are many alternatives, the phrase "one of" may precede a list of expansions given on a single line. This is simply shorthand for listing each of the alternatives on a separate line. [Example: The production:

```
real-type-suffix:: one of
    F f D d M m
```

is shorthand for:

```
real-type-suffix::
    F
    f
    D
    d
    M
    m
```

end example]

All terminal characters are to be understood as the appropriate Unicode character from the range U+0020 to U+007F, as opposed to any similar-looking characters from other Unicode character ranges.

### 7.2.3 Lexical grammar

The lexical grammar of C# is presented in §7.3, §7.4, and §7.5. The terminal symbols of the lexical grammar are the characters of the Unicode character set, and the lexical grammar specifies how characters are combined to form tokens (§7.4), white space (§7.3.4), comments (§7.3.3), and pre-processing directives (§7.5).

Every source file in a C# program shall conform to the input production of the lexical grammar (§7.3.1).

### 7.2.4 Syntactic grammar

The syntactic grammar of C# is presented in the clauses, subclauses, and annexes that follow this subclause. The terminal symbols of the syntactic grammar are the tokens defined by the lexical grammar, and the syntactic grammar specifies how tokens are combined to form C# programs.

Every source file in a C# program shall conform to the compilation-unit production (§14.2) of the syntactic grammar.

### 7.2.5 Grammar ambiguities

The productions for simple-name (§12.7.3) and member-access (§12.7.5) can give rise to ambiguities in the grammar for expressions. [Example: The statement:

```
F(G<A, B>(7));
```

could be interpreted as a call to F with two arguments, G < A and B > (7). Alternatively, it could be interpreted as a call to F with one argument, which is a call to a generic method G with two type arguments and one regular argument. end example]

If a sequence of tokens can be parsed (in context) as a simple-name (§12.7.3), member-access (§12.7.5), or pointer-member-access (§23.6.3) ending with a type-argument-list (§9.4.2), the token immediately following the closing > token is examined. If it is one of

- `(`
- `)`
- `]`
- `:`
- `;`
- `,`
- `.`
- `?`
- `==`
- `!=`

then the type-argument-list is retained as part of the simple-name, member-access, or pointer-member-access and any other possible parse of the sequence of tokens is discarded. Otherwise, the type-argument-list is not considered part of the simple-name, member-access, or pointer-member-access, even if there is no other possible parse of the sequence of tokens. [Note: These rules are not applied when parsing a type-argument-list in a namespace-or-type-name (§8.8). end note] [Example: The statement:

```
F(G<A, B>(7));
```

will, according to this rule, be interpreted as a call to F with one argument, which is a call to a generic method G with two type arguments and one regular argument. The statements

```
F(G<A, B>7);
F(G<A, B>>7);
```

will each be interpreted as a call to F with two arguments. The statement

```
x = F<A> + y;
```

## 7.3 Lexical analysis

### 7.3.1 General

The input production defines the lexical structure of a C# source file. Each source file in a C# program shall conform to this lexical grammar production.

```
input::
    input-section_opt

input-section::
    input-section-part
    input-section input-section-part

input-section-part::
    input-elements_opt new-line
    pp-directive

input-elements::
    input-element
    input-elements input-element

input-element::
    whitespace
    comment
    token
```

Five basic elements make up the lexical structure of a C# source file: Line terminators (§7.3.2), white space (§7.3.4), comments (§7.3.3), tokens (§7.4), and pre-processing directives (§7.5). Of these basic elements, only tokens are significant in the syntactic grammar of a C# program (§7.2.4), except in the case of a > token being combined with another token to form a single operator (§7.4.6).

The lexical processing of a C# source file consists of reducing the file into a sequence of tokens that becomes the input to the syntactic analysis. Line terminators, white space, and comments can serve to separate tokens, and pre-processing directives can cause sections of the source file to be skipped, but otherwise these lexical elements have no impact on the syntactic structure of a C# program.

When several lexical grammar productions match a sequence of characters in a source file, the lexical processing always forms the longest possible lexical element. [Example: The character sequence // is processed as the beginning of a single-line comment because that lexical element is longer than a single / token. end example]

### 7.3.2 Line terminators

Line terminators divide the characters of a C# source file into lines.

```
new-line::
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Carriage return character (U+000D) followed by line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)
```

For compatibility with source code editing tools that add end-of-file markers, and to enable a source file to be viewed as a sequence of properly terminated lines, the following transformations are applied, in order, to every source file in a C# program:

- If the last character of the source file is a Control-Z character (U+001A), this character is deleted.
- A carriage-return character (U+000D) is added to the end of the source file if that source file is non-empty and if the last character of the source file is not a carriage return (U+000D), a line feed (U+000A), a next line character (U+0085), a line separator (U+2028), or a paragraph separator (U+2029). [Note: The additional carriage-return allows a program to end in a pp-directive (§7.5) that does not have a terminating new-line. end note]

### 7.3.3 Comments

Two forms of comments are supported: delimited comments and single-line comments.

A delimited comment begins with the characters /* and ends with the characters */. Delimited comments can occupy a portion of a line, a single line, or multiple lines. [Example: The example

Comments do not nest. The character sequences /* and */ have no special meaning within a single-line comment, and the character sequences // and /* have no special meaning within a delimited comment.

Comments are not processed within character and string literals.

[Note: These rules must be interpreted carefully. For instance, in the example below, the delimited comment that begins before A ends between B and C(). The reason is that

// B */ C();

is not actually a single-line comment, since // has no special meaning within a delimited comment, and so */ does have its usual special meaning in that line.

Likewise, the delimited comment starting before D ends before E. The reason is that "D */ " is not actually a string literal, since it appears inside a delimited comment.

A useful consequence of /* and */ having no special meaning within a single-line comment is that a block of source code lines can be commented out by putting // at the beginning of each line. In general it does not work to put /* before those lines and */ after them, as this does not properly encapsulate delimited comments in the block, and in general may completely change the structure of such delimited comments.

Example code:

```
static void Main() {
    /* A
    // B */ C();
    Console.WriteLine(/* "D */ "E");
}
```

end note

### 7.3.4 White space

White space is defined as any character with Unicode class Zs (which includes the space character) as well as the horizontal tab character, the vertical tab character, and the form feed character.

```
whitespace::
    whitespace-character
    whitespace whitespace-character

whitespace-character::
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

## 7.4 Tokens

### 7.4.1 General

There are several kinds of tokens: identifiers, keywords, literals, operators, and punctuators. White space and comments are not tokens, though they act as separators for tokens.

```
token::
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```
