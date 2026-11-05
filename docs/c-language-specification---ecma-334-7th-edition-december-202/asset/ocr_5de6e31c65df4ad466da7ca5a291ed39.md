# D. Documentation comments

This annex is informative.

# D.1 General

C# provides a mechanism for programmers to document their code using a comment syntax that contains XML text. In source code files, comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede. Comments using such syntax are called documentation comments. They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method). The XML generation tool is called the documentation generator. (This generator could be, but need not be, the C# compiler itself.) The output produced by the documentation generator is called the documentation file. A documentation file is used as input to a documentation viewer; a tool intended to produce some sort of visual display of type information and its associated documentation.

A conforming C# compiler is not required to check the syntax of documentation comments; such comments are simply ordinary comments. A conforming compiler is permitted to do such checking, however.

This specification suggests a set of standard tags to be used in documentation comments, but use of these tags is not required, and other tags may be used if desired, as long as the rules of well-formed XML are followed. For C# implementations targeting the CLI, it also provides information about the documentation generator and the format of the documentation file. No information is provided about the documentation viewer.

# D.2 Introduction

Comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements that they precede. Such comments are Single-Line_Comments (§6.3.3) that start with three slashes (///), or Delimited_Comments (§6.3.3) that start with a slash and two asterisks (/**). They must immediately precede a user-defined type or a member that they annotate. Attribute sections (§22.3) are considered part of declarations, so documentation comments must precede attributes applied to a type or member.

For expository purposes, the format of document comments is shown below as two grammar rules: Single_Line_Doc_Comment and Delimited_Doc_Comment. However, these rules are not part of the C# grammar, but rather, they represent particular formats of Single_Line_Comment and Delimited_Comment lexer rules, respectively.

Syntax:

```
Single_Line_Doc_Comment
  : '///' Input_Character*
  ;

Delimited_Doc_Comment
```