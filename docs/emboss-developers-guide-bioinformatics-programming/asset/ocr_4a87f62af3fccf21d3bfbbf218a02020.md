# Appendix D Code documentation standards

# D.1 Introduction

The guidelines for code documentation cover:

+   • General comments documenting the source code
+   • Structured comments and licence information at the head of each application source file
+   • Structured comments and licence information at the head of each library source file
+   • Structured comments describing each function
+   • Structured comments describing each datatype (C structure definitions)

A particular style (see below) is recommended for general C-style comments within the code. Such comments are an informal but valuable way of documenting the code. For the main body of documentation, structured comments are used.

The approach taken is based broadly on JavaDoc. Embedded documentation is marked up with text tags which begin with @ followed by a code identifying the item, then the free documentation text. No text should be given before the @ although any leading asterisks (*) or spaces are stripped before parsing. For example:

```
** @source ApplicationName
```

Text following a tag on a line must not contain HTML markup (this would complicate parsers that convert the text to XML for use in generating the online documentation). The text after the tag continues until a new tag is reached or a token (*/) indicating the end of a C-style comment is found.

# D.2 General comments

Comments can make a program much easier to understand, but used heavily or poorly placed they can render good code unreadable. Use them conservatively. Good places to put comments include:

+   • Major logical steps within a program or function
+   • Tricky steps within a program or function
+   • Key variables, but do not document individual housekeeping variables, for example loop counters