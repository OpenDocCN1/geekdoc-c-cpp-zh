# Chapter 3

# A Closer Look: Programming Errors

but professionals don't. They understand that a runtime error is a flaw that can damage the reputation of the program and programmer.

To prevent compile-time and runtime errors, it is more fruitful to determine what causes them. As mentioned, compile-time errors are also called syntax errors: mistakes in the structure or spelling of a statement. For example, examine the following statements:

```
cout << "There are four syntax errors here\n\cot * Can you find them";
```

They contain the following syntax errors:

+   1. A closing quotation is missing in line 1.
2. A semicolon () is missing in line 1.
3. The keyword cout is misspelled in line 2.
4. The insertion operator, <<, is missing in line 2.

When the program is compiled, the compiler detects all these errors because they're syntax errors that violate the basic rules of C++. If they aren't detected by desk checking, the compiler detects them and displays an error message.¹ Sometimes the error message is clear and obvious; at other times, understanding the compiler's error message takes a little effort. Because syntax errors are the only type that can be detected at compile time, "compiler errors" and "syntax errors" are used interchangeably. Strictly speaking, compiler refers to when the error is detected, and syntax refers to the type of error detected.

The misspelling of "them" in the second statement is not a syntax error. Although this spelling error results in a undesirable output line, it's not a violation of C++'s rules. It's a typographical error, commonly referred to as a "typo". The compiler doesn't catch this type of typographical error.

Another error the compiler can't detect is a logic error, which can cause a runtime error or produce incorrect results. These errors are characterized by unexpected, or unintended output that is a direct result of failure in the program's logic. These errors can be detected by desk checking, by testing, by when a user gets erroneous output while the program is executing, or not at all. If the error is detected while the program is executing, a runtime error can occur that generates an error message, causes the program to terminate.

The most serious errors are caused by not fully understanding the program requirements because logic reflects the logic of which it's coded. For example, if a program's purpose is to make the calculation, what inputs are needed to perform the calculation, or what special conditions exist (such as temperature affects the beam), a logic error occurs. Because the compiler doesn't detect these errors they often go undetected at runtime, they are always more difficult to detect than syntax errors

> ¹They might, however, be detected at the same time. Frequently, one syntax error masks another error, and the second error is detected after the first is corrected.

> ²The misspelling of a C++ keyword or a declared variable name that results in an undeclared name is caught, however, because it results in a syntax error or an undeclared variable.