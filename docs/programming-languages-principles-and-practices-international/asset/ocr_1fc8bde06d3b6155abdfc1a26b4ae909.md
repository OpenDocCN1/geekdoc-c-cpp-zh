(continued)

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

# 8.10.3 Entering Type Information in Declarations

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

(continues)