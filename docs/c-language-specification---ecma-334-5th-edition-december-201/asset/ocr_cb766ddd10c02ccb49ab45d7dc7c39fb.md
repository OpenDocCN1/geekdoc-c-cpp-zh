# Annex D. Documentation comments

This annex is informative.

# D.1 General

C# provides a mechanism for programmers to document their code using a special comment syntax that contains XML text. In source code files, comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede. Comments using such syntax are called documentation comments. They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method). The XML generation tool is called the documentation generator. (This generator could be, but need not be, the C# compiler itself.) The output produced by the documentation generator is called the documentation file. A documentation file is used as input to a documentation viewer, a tool intended to produce some sort of visual display of type information and its associated documentation.

A conforming C# compiler is not required to check the syntax of documentation comments; such comments are simply ordinary comments. A conforming compiler is permitted to do such checking, however.

This specification suggests a set of standard tags to be used in documentation comments, but use of these tags is not required, and other tags may be used if desired, as long the rules of well-formed XML are followed. For C# implementations targeting the CLI, it also provides information about the documentation generator and the format of the documentation file. No information is provided about the documentation viewer.

# D.2 Introduction

Comments having a special form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede. Such comments are single-line comments that start with three slashes (///), or delimited comments that start with a slash and two stars (/**). They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method) that they annotate. Attribute sections (§22.3) are considered part of declarations, so documentation comments must precede attributes applied to a type or member.

# Syntax:

```
single-line-doc-comment::
/// input-characters_opt

delimited-doc-comment::
/** delimited-comment-text_opt */
```

In a single-line-doc-comment, if there is a whitespace character following the /// characters on each of the single-line-doc-comments adjacent to the current single-line-doc-comment, then that whitespace character is not included in the XML output.

In a delimited-doc-comment, if the first non-whitespace character on the second line is an asterisk and the same pattern of optional whitespace characters and an asterisk character is repeated at the beginning of each of the lines within the delimited-doc-comment, then the characters of the repeated pattern are not included in the XML output. The pattern can include whitespace characters after, as well as before, the asterisk character.

# Example: