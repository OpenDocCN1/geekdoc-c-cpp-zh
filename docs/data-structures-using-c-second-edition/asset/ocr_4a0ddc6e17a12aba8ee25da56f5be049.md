```
main()
{
    Statement 1;
    Statement 2;
    ......
    ......
    Statement N;
}
Function1()
{
    Statement 1;
    Statement 2;
    ......
    Statement N;
}
Function2()
{
    Statement 1;
    Statement 2;
    ......
    Statement N;
}
......
......
FunctionN()
{
    Statement 1;
    Statement 2;
    ......
    Statement N;
}
```

Figure 1.1 Structure of a C program

of statements arranged according to specific meaningful sequence. Note that programmers can choose any name for functions. It is not mandatory to write Function1, Function2, etc., with an exception that every program must contain one function that has its name as `main()`.

# 1.2 IDENTIFIERS AND KEYWORDS

Every word in a C program is either an identifier or a keyword.

# Identifiers

Identifiers are basically names given to program elements such as variables, arrays, and functions. They are formed by using a sequence of letters (both uppercase and lowercase), numerals, and underscores. Following are the rules for forming identifier names:

+   - Identifiers cannot include any special characters or punctuation marks (like #, $, ^, ?, ., etc.) except the underscore “_”.
+   - There cannot be two successive underscores.
+   - Keywords cannot be used as identifiers.
+   - The case of alphabetic characters that form the identifier name is significant. For example, “FIRST” is different from ‘first’ and ‘First’.
+   - Identifiers must begin with a letter or an underscore. However, use of underscore as the first character must be avoided because several compiler-defined identifiers in the standard C library have underscore as their first character. So, inadvertently duplicated names may cause definition conflicts.
+   - Identifiers can be of any reasonable length. They should not contain more than 31 characters. (They can actually be longer than 31, but the compiler looks at only the first 31 characters of the name.)

# Keywords

Like every computer language, C has a set of reserved words often known as keywords that cannot be used as an identifier. All Keywords are basically a sequence of characters that have a fixed meaning. By convention, all keywords must be written in lower case letters. Table 1.1 contains the list of keywords in C.

| auto | break | case | char | const | continue | default | do |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| double | else | enum | extern | float | for | goto | if |
| int | long | register | return | short | signed | sizeof | static |
| struct | switch | typedef | union | unsigned | void | volatile | while |

# 1.3 BASIC DATA TYPES

Data type determines the set of values that a data item can take and the operations that can be performed on the item. C language provides four basic data types. Table 1.2 lists the data types, their size, range, and usage for a C programmer.

The char data type is of one byte and is used to store single characters. Note that C does not provide any data type for storing text. This is because text is made up of individual characters. You