# 1.3. Book Organization

We start from the top, in terms of the general C# program. A C# program is essentially a collection of C# source files that are (to be) compiled together. An executable C# program has one and only entry point, which could be a Main method of a startup class or the top-level statements in one source code file. We also describe the basic concepts of access e.g., public vs namespaces, and blocks and scopes in this chapter.

A source code file is essentially a sequence of characters. We next go through some basic process of converting an input sequence of characters to a sequence of "tokens" which the compiler understands. This is generally known as "lexing". C#'s lexical structure is rather similar to those of other C-style programming languages.

A C# program logically consists of one or more A namespace can include other namespaces or declarations of custom types, e.g., using and etc., which can in turn include other member declarations. In C#, the using directives are used to import names from other namespaces. Namespaces themselves do not participate in access control.

C# types are organized in a hierarchy with the base class object at its root. As with many C-style languages, C# has values and references (or, pointers), with different characteristics. C# supports two distinct, and mutually exclusive, categories of types, namely, value types and reference In addition, C# includes the dynamic which is sort of an escape hatch when static typing is too limiting in certain cases.