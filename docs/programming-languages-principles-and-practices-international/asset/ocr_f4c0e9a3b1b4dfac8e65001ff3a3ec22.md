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