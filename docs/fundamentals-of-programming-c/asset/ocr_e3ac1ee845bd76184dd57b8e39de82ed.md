# 3.3. IDENTIFIERS

better than the equally permissible, s, and u. A variable's name should be related to its purpose within the program. Good variable names make programs more readable by humans. Since programs often contain many variables, well-chosen variable names can render an otherwise obscure collection of symbols more understandable.

C++ has strict rules for variables. A variable name is one example of an identifier. An identifier is a word used to name things. One of the identifiers can name a variable. We will see in later chapters that identifiers name other things such as functions and classes. Identifiers have the following form:

+   - Identifiers must contain at least one character.
- The first character must be an alphabetic letter (upper or lower case) or the underscore
`ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz_`
- The remaining characters (any) may be alphabetic characters (upper or lower case), or a digit
`ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefdefghjklnopqrstuvwxyz_0123456789`
- No other characters (including spaces) are permitted in identifiers.
- A reserved word cannot be used as an identifier (see Table 3.1).

Here are some examples of valid and invalid identifiers:

+   - All of the following words are valid identifiers and so qualify as variable: **x, x2, total, port_22**, and **FLAG**.
- None of the following words are valid identifiers: **sub-total** (dash is not a legal symbol in an identifier), **first entry** (space is not a legal symbol in an identifier), **4all** (begins with a digit), **#** (pound is not a legal symbol in an identifier), and **class** (class is a reserved word).

C++ has many reserved words for which could otherwise be used as identifiers. Reserved words are special and are used to define the structure of C++ programs. Table 3.1 lists all the C++ reserved words.

The purposes of these reserved words are revealed throughout this book.
You may not use them but if you accidentally attempt to use one of the reserved words in a program as a variable name, the compiler will issue an error (see Section 4.6 for more compiler errors).

In Listing 2.1 (simple.cpp) we used reserved words: **using, namespace**, and **int**. Note that **include, endl,** and **main** are reserved words.

Some programming languages do not require programmers to declare variables before they are used; the type of a variable is determined by how it is used. Some languages allow the same variable to assume different types in different parts of a program. Such languages are known as dynamically-typed languages. C++ is a statically-typed language. In a statically-typed language, the type of a variable must be explicitly specified before it is used in a program. While the requirement to declare all variables may initially seem like a minor annoyance, it offers several advantages.

+   - When variables are declared, the compiler can catch typographical errors that dynamically-typed languages cannot. For example, consider the following section of code: