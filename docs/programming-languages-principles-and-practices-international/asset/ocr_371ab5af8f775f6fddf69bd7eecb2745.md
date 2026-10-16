Note how the use of the expression ROW_MAX * 2 in the definition of COLUMN_MAX maintains a 2:1 aspect ratio of the matrix dimensions, allowing the programmer to vary their size by changing just the value of ROW_MAX.

The following grammar rules for the two types of declarations show the placements of the static expressions in them:

numberDeclaration = identifierList ":" "constant" ":=" <static>expression ";"

range = "range" <static>simpleExpression ".." <static>simpleExpression

Syntactically, static expressions look just like other expressions. Their semantics are also similar, in that the applications of the arithmetic, comparison, and logical operators produce the expected results. However, to ensure that these results can be computed at compile time, static expressions cannot include variable or parameter references.

In TinyAda, the values of static expressions ultimately come from literals in the token stream, or from the values of constant names, including the two built-in symbolic constants, TRUE and FALSE. The two types of literals include integer and character values. The scanner translates the different source code representations of these to a single internal form—base 10 integers for all of the TinyAda integer representations and ASCII values for the 128 character literals. The internal forms of the two Boolean values are, by convention, the integers 0 for FALSE and 1 for TRUE. The parser uses these internal representations to evaluate all static expressions, as you will see shortly.

# 9.6.2 Entering the Values of Symbolic Constants

Each symbolic constant now has a value attribute in its symbol entry record. The method setValue installs this value, which must be an integer, for a list of constant identifiers. For example, when symbol entries for the built-in names TRUE and FALSE are initialized, their values must be entered as well:

```
private void initTable(){
    ...
    entry = table.enterSymbol("TRUE");
    entry.setRole(SymbolEntry.CONST);
    entry.setType(BOOL_TYPE);
    entry.setValue(1);                // TRUE = 1, internally
    entry = table.enterSymbol("FALSE");
    entry.setRole(SymbolEntry.CONST);
    entry.setType(BOOL_TYPE);
    entry.setValue(0);                // FALSE = 0, internally
}
```

The method numberOrObjectDeclaration must also install a value for the list of constant identifiers just processed. Working top-down, we assume that the method that parses the TinyAda expression