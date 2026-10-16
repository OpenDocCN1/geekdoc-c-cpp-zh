
# CHAPTER

# Syntax

+   6.1    Lexical Structure of Programming Languages    204
+   6.2    Context-Free Grammars and BNFs    208
+   6.3    Parse Trees and Abstract Syntax Trees    213
+   6.4    Ambiguity, Associativity, and Precedence    216
+   6.5    EBNFs and Syntax Diagrams    220
+   6.6    Parsing Techniques and Tools    224
+   6.7    Lexics vs. Syntax vs. Semantics    235
+   6.8    Case Study: Building a Syntax Analyzer for TinyAda    237

# CHAPTER 6

Syntax is the structure of a language. In Chapter 1, we noted the difference between the syntax and semantics of a programming language. In the early days of programming languages, both the syntax and semantics of a language were described by lengthy English explanations and many examples. While the semantics of a language are still usually described in English, one of the great advances in programming languages has been the development of a formal system for describing syntax that is now almost universally in use. In the 1950s, Noam Chomsky developed the idea of context-free grammars, and John Backus, with contributions by Peter Naur, developed a notational system for describing these grammars that was used for the first time to describe the syntax of Algol60. These **Backus-Naur forms—BNFs for short—have subsequently been used in the definition of many programming languages, including C, Java, and Ada. Indeed, every modern programmer and computer scientist needs to know how to read, interpret, and apply BNF descriptions of language syntax. BNFs occur with minor textual variations in three basic forms: original BNF; extended BNF (EBNF), popularized by Niklaus Wirth (and very briefly used to describe the syntax of Scheme in Chapter 3); and syntax diagrams.

In Section 6.1, we briefly look at lexical structures, which are the building blocks on which syntax is often based. We also explore the process of scanning, or recognizing, lexical structure. In Section 6.2, we introduce context-free grammars and their description in BNF. In Section 6.3, we describe the representation of syntactic structure using trees. In Section 6.4, we consider a few of the issues that arise in constructing BNFs for a programming language. EBNFs and syntax diagrams are introduced in Section 6.5. In Section 6.6, we discuss the basic technique of recursive-descent parsing and its close relationship to EBNF and syntax diagrams and briefly look at YACC/Bison, a standard tool for analyzing grammars and constructing parsers. In Section 6.7, we examine the sometimes hazy boundaries among the lexical, syntactic, and semantic structures of a programming language. Finally, Section 6.8 puts some of these ideas to work by developing a syntax analyzer for a small programming language.

## 6.1 Lexical Structure of Programming Languages

The **lexical structure** of a programming language is the structure of its **tokens**, or words. A language’s lexical structure and its syntactic structure are two different things, but they are closely related. Typically, during its **scanning** phase, a translator collects sequences of characters from the input program and forms them into tokens. During its **parsing** phase, the translator then processes these tokens, thereby determining the program’s syntactic structure.

Tokens generally fall into several distinct categories. Typical token categories include the following:

- **reserved words**, sometimes called **keywords**, such as **if** and **while**
- **literals** or **constants**, such as 42 (a numeric literal) or "hello" (a string literal)
- **special symbols**, such as ";", "<=", or "+"
- **identifiers**, such as x24, monthly_balance, or putchar

Reserved words are so named because an identifier cannot have the same character string as a reserved word. Thus, in C, the following variable declaration is illegal because **if** is a reserved word:

```
double if;
```

Sometimes programmers are confused about the difference between reserved words and **predefined identifiers**, or identifiers that have been given an initial meaning for all programs in the language but that are capable of redefinition. (To add to the confusion, sometimes these identifiers are also called keywords.) Examples of predefined identifiers are all standard data types in Ada, such as **integer** and **boolean**, and in Python, such as **round** and **print**. See Section 6.7 for more on this phenomenon.

In some older languages identifiers had a fixed maximum size, while in most contemporary languages identifiers can have arbitrary length. Occasionally, even when arbitrary-length identifiers are allowed, only the first six or eight characters are guaranteed to be significant. (You can see how this can be a source of confusion for programmers.)

A problem arises in determining the end of a variable-length token such as an identifier and in distinguishing identifiers from reserved words. As an example, the sequence of characters:

```
doif
```

in a program could be either the two reserved words do and **if** or the identifier **doif**. Similarly, the string x12 could be a single identifier or the identifier x and the numeric constant 12. To eliminate this ambiguity, it is a standard convention to use the **principle of longest substring** in determining tokens (sometimes called the principle of “maximum munch”). The principle works like this: At each point, the longest possible string of nonblank characters is collected into a single token. This means that **doif** and x12 are always identifiers. It also means that intervening characters, even blanks, can make a difference. Thus, in most languages:

```
do if
```

is not an identifier; instead, it is the two reserved words do and **if**.

The format of a program can affect the way tokens are recognized. For example, as you just saw, the principle of longest substring requires that certain tokens be separated by **token delimiters** or **white space**. The end of a line of text can be doubly meaningful because it can be white space, but it can also mean the end of a structural entity. Indentation can also be used in a programming language to determine structure. In fact, Python’s simple syntax rests on the significance of indentation.

A **free-format** language is one in which format has no effect on the program structure (other than to satisfy the principle of longest substring). Most modern languages are free format, but a few have significant format restrictions. Rarely is a language **fixed format**, in which all tokens must occur in prespecified locations on the page.

Tokens in a programming language are often described in English, but they can also be described formally by **regular expressions**, which are descriptions of patterns of characters. Regular expressions have three basic operations: concatenation, repetition, and choice or selection. Repetition is indicated by the use of an asterisk after the item to be repeated, choice is indicated by a vertical bar between the items from which the selection is to be made, and concatenation is given simply by sequencing the items without an explicit operator. Parentheses are also often included to allow for the grouping of operations. For example, `(a|b)*c` is a regular expression indicating 0 or more repetitions of either the characters a or b (choice), followed by a single character c (concatenation); strings that match this regular expression include ababaac, aac, babbc, and just c itself, but not aaaab or bca.

Regular expression notation is often extended by additional operations and special characters to make them easier to write. For example, square brackets with a hyphen indicate a range of characters, + indicates one or more repetitions, ? indicates an optional item, and a period indicates any character. With these notations, we can write compact regular expressions for even fairly complex tokens. For example,

```
[0–9]+
```

is a regular expression for simple integer constants consisting of one or more digits (characters between 0 and 9). Also, the regular expression:

```
[0–9]+(\\.[0–9]+)?
```

describes simple (unsigned) floating-point literals consisting of one or more digits followed by an optional fractional part consisting of a decimal point (with a backslash, or escape, character in front of it to remove the special meaning of a period as matching any character), followed again by one or more digits.

Many utilities use regular expressions in text searches. This is true of most modern text editors, as well as various file search utilities, such as UNIX grep (“global regular expression print”). The UNIX lex utility can also be used to automatically turn a regular expression description of the tokens of a language into a scanner. (A successor to lex, called flex, or fast lex, is freely available and runs on most operating systems.)

While a study of lex/flex and the use of regular expressions to construct scanners is beyond the scope of this text, in simple cases, scanners can be constructed by hand relatively easily. To give you a sense of such a scanner construction, we present C code for a simple scanner in Figure 6.1. There are six tokens in this language (represented as constants of an enumeration type, lines 4–5): integer constants consisting of one or more digits; the special characters +, *, (, and ); and the end of line token (represented in C or Java as the special character `\\n`, or newline). Such a language may be used to specify a simple integer arithmetic expression with addition and multiplication on a single line of input, such as

```
(2 + 34) * 42
```

Blanks are to be skipped, and any character (such as a or # or –) that is not specified is to be considered an error (thus, the need for the additional ERROR token on line 5).

Before closing this section and moving on to the study of syntax and parsing, we note the following additional features of the code in Figure 6.1. First, the code contains a main function (lines 31–47) to test drive the scanner (which is represented by the getToken function, lines 8–30). Given a line of input, the main function simply calls getToken repeatedly and prints each token as it is recognized; a number is also printed with its numeric value, and an error is printed with the offending character. Second, we note
