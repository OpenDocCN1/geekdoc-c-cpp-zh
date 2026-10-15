# # APPENDIX F Java Coding Guidelines



# ### A. Identifier Naming

+   1. Give identifiers semantic meaning. For example, do not use single letter names such as a or i unless the single letter has semantic meaning.

+   2. Make identifiers easy to read. For example, use currentValue instead of curval.

+   3. Keep identifiers to a reasonably short length.

+   4. Use the underscore character to separate words of a constant.

# ### B. Identifier Case

+   1. Use UPPERCASE for constants.

+   2. Use Title Case for class, package, and interface names.

+   3. Use lowercase for variable and method names, except for the first letter of each word other than the first word. For example, minTaxRate. Note that all reserved words must be lowercase.

# ### C. Indentation

+   1. Indent the code in any block by three or four spaces (be consistent).

+   2. If the body of a loop, if statement, or else clause is a single statement (not a block), indent the statement three spaces on its own line.

+   3. Put the left brace ({) starting each new block on a new line. Line up the terminating right brace (}) with the opening left brace. For example:

```
```java
while (value < 25)
{
    value += 5;
    System.out.println("The value is " + value);
}
```
```

+   4. In a switch statement, indent each case label three spaces. Indent all code associated with a case three additional spaces.

# ### D. Spacing

+   1. Carefully use white space to draw attention to appropriate features of a program.

+   2. Put one space after each comma in a parameter list.

+   3. Put one space on either side of a binary operator.

+   4. Do not put spaces immediately after a left parenthesis or before a right parenthesis.

+   5. Do not put spaces before a semicolon.

+   6. Put one space before a left parenthesis, except before an empty parameter list.