(continued)

```
SymbolEntry list = identifierList();
list.setRole(SymbolEntry.CONST);
EnumDescriptor t = new EnumDescriptor();
t.setIdentifiers(list);
list.setType(t);
accept(Token.R_PAR, ")"' expected");
return t;
}
```

The method now returns a type descriptor. The three new lines of code in the middle of the method

+   - Instantiate a type descriptor for an enumerated type.
+   - Set its identifiers attribute to the list of identifiers just parsed.
+   - Set the type of these identifiers to the type descriptor just created.

The processing of array and subrange type definitions is similar and left as an exercise for the reader.

# 8.10.4 Checking Types of Operands in Expressions

A quick glance at the rules for TinyAda expressions gives some hints as to how their types should be checked. Working top-down, a condition must be a Boolean expression, so clearly the expression method must return a type descriptor to be checked. Here is the new code for the condition method:

```
/*
condition = <boolean>expression
*/
private void condition(){
    TypeDescriptor t = expression();
    matchTypes(t, BOOL_TYPE, "Boolean expression expected");
}
```

The expression method in turn might see two or more relations separated by Boolean operators. Thus, the relation method must also return a type descriptor. If a Boolean operator is detected in the expression method, then the types of the two relations must each be matched against the parser's BOOL_TYPE variable.

The coder of the parser must read each syntax rule for expressions carefully and add the appropriate code for type checking to the corresponding method. As an example, here is the code for the method factor, which shows the checking of some operands as well as the return of the appropriate type descriptor: