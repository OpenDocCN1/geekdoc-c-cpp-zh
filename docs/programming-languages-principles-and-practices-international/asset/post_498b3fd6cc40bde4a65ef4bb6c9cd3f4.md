
(continued)

```
INT_TYPE.setSuperType(INT_TYPE);
}

// Attach type information to the built-in identifiers
private void initTable(){
    table = new SymbolTable(chario);
    table.enterScope();
    SymbolEntry entry = table.enterSymbol("BOOLEAN");
    entry.setRole(SymbolEntry.TYPE);
    entry.setType(BOOL_TYPE);
    entry = table.enterSymbol("CHAR");
    entry.setRole(SymbolEntry.TYPE);
    entry.setType(CHAR_TYPE);
    entry = table.enterSymbol("INTEGER");
    entry.setRole(SymbolEntry.TYPE);
    entry.setType(INT_TYPE);
    entry = table.enterSymbol("TRUE");
    entry.setRole(SymbolEntry.CONST);
    entry.setType(BOOL_TYPE);
    entry = table.enterSymbol("FALSE");
    entry.setRole(SymbolEntry.CONST);
    entry.setType(BOOL_TYPE);
}
```

The parser also defines two utility methods to check types. The first, matchTypes, compares two type descriptors for compatibility using name equivalence. The second, acceptTypeForm, compares a type descriptor's type form to an expected type form. Each method outputs an error message if a type error occurs, as shown in the following code:

```
// Compares two types for compatibility using name equivalence
private void matchTypes(TypeDescriptor t1, TypeDescriptor t2,
                        String errorMessage){
    // Need two valid type descriptors to check for an error
    if (t1.form == TypeDescriptor.NONE || t2.form == TypeDescriptor.NONE)
        return;
    // Exact name equivalence: the two descriptors are identical
    if (t1 == t2) return;
    // To check two subranges, the supertypes must be identical
    if (t1.form == TypeDescriptor.SUBRANGE && t2.form == TypeDescriptor.SUBRANGE){
        if (((SubrangeDescriptor)t1).superType != ((SubrangeDescriptor)t2).superType)
            chario.putError(errorMessage);
    }
    else
```

```
// Otherwise, at least one record, array, or enumeration does not match
chario.putError(errorMessage);
}

// Checks the form of a type against an expected form
private void acceptTypeForm(TypeDescriptor t, int typeForm, String errorMessage){
    if (t.form == TypeDescriptor.NONE) return;
    if (t.form != typeForm)
        chario.putError(errorMessage);
}
```

Note that the formal type descriptor parameters of these two methods are declared to be of the class TypeDescriptor, which allows the methods to receive objects of any of the type descriptor subclasses as actual parameters. Both methods then check type forms to determine which actions to take. If the form is NONE, a semantic error has already occurred somewhere else, so the methods quit to prevent a ripple effect of error messages. Otherwise, further checking occurs. In the case of matchTypes, Java’s == operator is used to detect the object identity of the two type descriptors. This can be done without knowing which classes these objects actually belong to. However, if the two descriptors are not identical, the types will be compatible only if they are both subranges and their supertypes are identical. After determining that the form of the two descriptors is SUBRANGE, the TypeDescriptor objects must be cast down to the SubrangeDescriptor class before accessing their supertype fields. Fortunately, this type of downcasting will rarely occur again in the parser; the use of TypeDescriptor as a parameter type and a method return type will provide very clean, high-level communication channels between the parsing methods.

## 8.10.3 Entering Type Information in Declarations

Type information must now be entered wherever identifiers are declared in a source program. We noted these locations in Section 8.8, where the parser enters identifier role information. The type information comes either from type identifiers (in number or object declarations, parameter specifications, and record component declarations) or from a type definition. In the case of a type identifier, the type descriptor is already available and is simply accessed in the identifier’s symbol entry. In the case of a type definition, a new type might be created. Therefore, the typeDefinition method should return to its caller the TypeDescriptor for the type just processed. The following code shows the implementation of this method and its use in the method TypeDeclaration, which declares a new type name:

```
/*
typeDeclaration = "type" identifier "is" typeDefinition ";"
*/
private void typeDeclaration(){
    accept(Token.TYPE, "'type' expected");
    SymbolEntry entry = enterId();
    entry.setRole(SymbolEntry.TYPE);
```

```
```java
accept(Token.IS, "'is' expected");
entry.setType(typeDefinition());        // Pick up the type
descriptor here
accept(Token.SEMI, "semicolon expected");
}

/*
typeDefinition = enumerationTypeDefinition | arrayTypeDefinition
                | range | <type>name
*/
private TypeDescriptor typeDefinition(){
    TypeDescriptor t = new TypeDescriptor();
    switch (token.code){
        case Token.ARRAY:
            t = arrayTypeDefinition();
            break;
        case Token.L_PAR:
            t = enumerationTypeDefinition();
            break;
        case Token.RANGE:
            t = range();
            break;
        case Token.ID:
            SymbolEntry entry = findId();
            acceptRole(entry, SymbolEntry.TYPE, "type name expected");
            t = entry.type;
            break;
        default: fatalError("error in type definition");
    }
    return t;
}
```
```

Note how each lower-level parsing method called in the **typeDefinition** method also returns a type descriptor, which is essentially like a buck being passed back up the call tree of the parsing process. We see the buck stopping at one point, when the type definition is just another identifier, whose type descriptor is accessed directly. The strategy of passing a type descriptor up from lower-level parsing methods is also used in processing expressions, as we will see shortly.

The next example shows how a new type is actually created. An enumeration type consists of a new set of constant identifiers. Here is the code for the method enumerationTypeDefinition:

```
```java
/*
enumerationTypeDefinition = "(" identifierList ")"
*/
private TypeDescriptor enumerationTypeDefinition(){
    accept(Token.L_PAR, "'(' expected");
```
```

```
SymbolEntry list = identifierList();
list.setRole(SymbolEntry.CONST);
EnumDescriptor t = new EnumDescriptor();
t.setIdentifiers(list);
list.setType(t);
accept(Token.R_PAR, ")' expected");
return t;
}
```

The method now returns a type descriptor. The three new lines of code in the middle of the method

- Instantiate a type descriptor for an enumerated type.
- Set its identifiers attribute to the list of identifiers just parsed.
- Set the type of these identifiers to the type descriptor just created.

The processing of array and subrange type definitions is similar and left as an exercise for the reader.

## 8.10.4 Checking Types of Operands in Expressions

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
