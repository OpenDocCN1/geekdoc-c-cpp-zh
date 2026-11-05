> *Note: These convenience rules are exceptions to the usual practice of not providing explicit token names for tokens defined by literal strings. end note*

The input production defines the lexical structure of a C# compilation unit.

```
input
  : input_section?
  ;

input_section
  : input_section_part+
  ;

input_section_part
  : input_element* New_Line
  | PP_Directive
  ;

input_element
  : Whitespace
  | Comment
  | token
  ;
```

> *Note: The above grammar is described by ANTLR parsing rules, it defines the lexical structure of a C# compilation unit and not lexical tokens. end note*

Five basic elements make up the lexical structure of a C# compilation unit: Line terminators (§6.3.2), white space (§6.3.4), comments (§6.3.3), tokens (§6.4), and pre-processing directives (§6.5). Of these basic elements, only tokens are significant in the syntactic grammar of a C# program (§6.2.4).

The lexical processing of a C# compilation unit consists of reducing the file into a sequence of tokens that becomes the input to the syntactic analysis. Line terminators, white space, and comments can serve to separate tokens, and pre-processing directives can cause sections of the compilation unit to be skipped, but otherwise these lexical elements have no impact on the syntactic structure of a C# program.

When several lexical grammar productions match a sequence of characters in a compilation unit, the lexical processing always forms the longest possible lexical element.

> *Example: The character sequence // is processed as the beginning of a single-line comment because that lexical element is longer than a single / token. end example*

Some tokens are defined by a set of lexical rules; a main rule and one or more sub-rules. The latter are marked in the grammar by fragment to indicate the rule defines part of another token. Fragment rules are not considered in the top-to-bottom ordering of lexical rules.

> *Note: In ANTLR fragment is a keyword which produces the same behavior defined here. end note*

# 6.3.2 Line terminators

Line terminators divide the characters of a C# compilation unit into lines.

```
New_Line
  : New_Line_Character
  | '\u000D\u000A'  // carriage return, line feed
  ;
```