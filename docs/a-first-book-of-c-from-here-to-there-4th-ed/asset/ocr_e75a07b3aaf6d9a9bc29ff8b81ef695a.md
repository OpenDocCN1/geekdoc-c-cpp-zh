syntax errors are detected only at compile time. Strictly speaking, however, "compile time" refers to when the error is detected, and "syntax" refers to the type of error detected.

Note that the misspelling of "them" in the second statement isn't a syntax error. Although this spelling error results in displaying an undesirable output line, it's not a violation of C++'s syntax rules. It's simply a typographical error, commonly referred to as a "typo." The compiler doesn't catch this type of typographical error.

Another error the compiler doesn't catch is a logic error, which is characterized by erroneous, unexpected, or unintentional output that's a result of some flaw in the program's logic. These errors can be detected by desk checking, by program testing, by accident when a user gets erroneous output while the program is running, or not at all.

The most serious logic error is caused by not fully understanding the program's requirements because the logic in a program reflects the logic on which it's coded. For example, if a program's purpose is to calculate a mortgage payment on a house or the load-bearing strength of a steel beam and the programmer doesn't fully understand how to make the calculation, what inputs are needed to perform the calculation, or what special conditions exist (such as what happens when someone makes an extra mortgage payment or how temperature affects the beam), a logic error occurs. Because the compiler doesn't detect these errors and they often go undetected at runtime, they are always more difficult to detect than syntax errors.

If logic errors are detected, typically they're revealed in one of two main ways. First, the program executes to completion but produces incorrect results, such as the following:

+   - No output—This result is caused by omitting an output statement or using a sequence of statements that inadvertently bypasses an output statement.

+   - Unappealing or misaligned output—This result is caused by an error in an output statement.

+   - Incorrect numerical results—This result is caused by assigning incorrect values to variables in an expression, coding an incorrect or incomplete algorithm, coding a correct algorithm incorrectly, omitting a statement, making a round-off error, or using an improper sequence of statements.

Second, a logic error can cause a runtime error. Examples of this type of logic error are attempts to divide by zero or take the square root of a negative number. Typically, these errors are caused by incorrect user input. Although beginning programmers tend to blame users for runtime errors caused by entering incorrect data, professionals don't. They understand that a runtime error is a basic flaw in the program's construction that can damage the reputation of both the program and the programmer. They also understand that determining the error and correcting what caused it are more fruitful than determining who caused it.

# Testing and Debugging

Program testing should be well thought out to maximize the possibility of locating errors. In this regard, an important programming realization is that although a single test can reveal the presence of an error, it does not verify the absence of one. In other words, the fact that a