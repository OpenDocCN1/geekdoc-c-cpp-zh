
## 10.6.10 Method Body

The method-body of a method declaration consists of either a block or a semicolon.

Abstract and external method declarations do not provide a method implementation, so their method bodies simply consist of a semicolon. For any other method, the method body is a block (§8.2) that contains the statements to execute when that method is invoked.

When the return type of a method is void, return statements (§8.9.4) in that method's body are not permitted to specify an expression. If execution of the method body of a void method completes normally (that is, if control flows off the end of the method body), that method simply returns to its caller.

When the return type of a method is not void, each return statement in that method's body must specify an expression that is implicitly convertible to the return type. The end point of the method body of a value-returning method must not be reachable. In other words, in a value-returning method, control is not permitted to flow off the end of the method body.

In the example

```
class A
{
    public int F() {}    // Error: return value required
    public int G() {
        return 1;
    }
    public int H(bool b) {
        if (b) {
            return 1;
        } else {
            return 0;
        }
    }
}
```

the value-returning F method results in a compile-time error because control can flow off the end of the method body. The G and H methods are correct because all possible execution paths end in a return statement that specifies a return value.

## 10.6.11 Method Overloading

The method overload resolution rules are described in §7.5.2.

## 10.7 Properties

A property is a member that provides access to a characteristic of an object or a class. Examples of properties include the length of a string, the size of a font, the caption of a window, the name of a customer, and so on. Properties are a natural extension of fields— both are named members with associated types, and the syntax for accessing fields and properties is the same. However, unlike fields, properties do not denote storage locations. Instead, properties have accessors that specify the statements to be executed when their values are read or written. Properties thus provide a mechanism for associating actions with the reading and writing of an object's attributes; furthermore, they permit such attributes to be computed.

Properties are declared using property-declarations:

```
property-declaration:
    attributes_opt property-modifiers_opt type member-name { accessor-declarations }

property-modifiers:
    property-modifier
    property-modifiers property-modifier

property-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

member-name:
    identifier
    interface-type . identifier
```

A property-declaration may include a set of attributes (§17), a valid combination of the four access modifiers (§10.3.5), and the new (§10.3.4), static (§10.6.2), virtual (§10.6.3), override (§10.6.4), sealed (§10.6.5), abstract (§10.6.6), and extern (§10.6.7) modifiers.

Property declarations are subject to the same rules as method declarations (§10.6) with regard to valid combinations of modifiers.

The *type* of a property declaration specifies the type of the property introduced by the declaration, and the *member-name* specifies the name of the property. Unless the property is an explicit interface member implementation, the *member-name* is simply an identifier. For an explicit interface member implementation (§13.4.1), the *member-name* consists of an *interface-type* followed by a “.” and an identifier.

The *type* of a property must be at least as accessible as the property itself (§3.5.4).

The *accessor-declarations*, which must be enclosed in “{” and “}” tokens, declare the accessors (§10.7.2) of the property. The accessors specify the executable statements associated with reading and writing the property.

Even though the syntax for accessing a property is the same as that for a field, a property is not classified as a variable. Thus it is not possible to pass a property as a ref or out argument.

When a property declaration includes an extern modifier, the property is said to be an *external property*. Because an external property declaration provides no actual implementation, each of its accessor-declarations consists of a semicolon.

### 10.7.1 Static and Instance Properties

When a property declaration includes a static modifier, the property is said to be a *static property*. When no static modifier is present, the property is said to be an *instance property*.

A static property is not associated with a specific instance, and it is a compile-time error to refer to this in the accessors of a static property.

An instance property is associated with a given instance of a class, and that instance can be accessed as this (§7.6.7) in the accessors of that property.

When a property is referenced in a *member-access* (§7.6.4) of the form E.M, if M is a static property, E must denote a type containing M; if M is an instance property, E must denote an instance of a type containing M.

The differences between static and instance members are discussed further in §10.3.7.

### 10.7.2 Accessors

The accessor-declarations of a property specify the executable statements associated with reading and writing that property.

```
accessor-declarations:
    get-accessor-declaration  set-accessor-declaration_opt
    set-accessor-declaration  get-accessor-declaration_opt

get-accessor-declaration:
    attributes_opt  accessor-modifier_opt  get  accessor-body

set-accessor-declaration:
    attributes_opt  accessor-modifier_opt  set  accessor-body

accessor-modifier:
    protected
    internal
    private
    protected  internal
    internal  protected

accessor-body:
    block
    ;
```

The accessor declarations consist of a get-accessor-declaration, a set-accessor-declaration, or both. Each accessor declaration consists of the token get or set followed by an optional accessor-modifier and an accessor-body.

The use of accessor-modifiers is governed by the following restrictions:

- An accessor-modifier may not be used in an interface or in an explicit interface member implementation.
- For a property or indexer that has no override modifier, an accessor-modifier is permitted only if the property or indexer has both a get and set accessor, and then is permitted on only one of those accessors.
- For a property or indexer that includes an override modifier, an accessor must match the accessor-modifier, if any, of the accessor being overridden.
- The accessor-modifier must declare an accessibility that is strictly more restrictive than the declared accessibility of the property or indexer itself. To be precise:
- If the property or indexer has a declared accessibility of public, the accessor-modifier may be either protected internal, internal, protected, or private.
- If the property or indexer has a declared accessibility of protected internal, the accessor-modifier may be either internal, protected, or private.
- If the property or indexer has a declared accessibility of internal or protected, the accessor-modifier must be private.
- If the property or indexer has a declared accessibility of private, no accessor-modifier may be used.

For abstract and extern properties, the accessor-body for each accessor specified is simply a semicolon. A non-abstract, non-extern property may be an automatically implemented property, in which case both get and set accessors must be given, both with a semicolon body (§10.7.3). For the accessors of any other non-abstract, non-extern property, the accessor-body is a block that specifies the statements to be executed when the corresponding accessor is invoked.

A get accessor corresponds to a parameterless method with a return value of the property type. Except as the target of an assignment, when a property is referenced in an expression, the get accessor of the property is invoked to compute the value of the property (§7.1.1). The body of a get accessor must conform to the rules for value-returning methods described in §10.6.10. In particular, all return statements in the body of a get accessor must specify an expression that is implicitly convertible to the property type. Furthermore, the end point of a get accessor must not be reachable.

A set accessor corresponds to a method with a single value parameter of the property type and a void return type. The implicit parameter of a set accessor is always named value. When a property is referenced as the target of an assignment (§7.17) or as the operand of ++ or -- (§7.6.9, §7.7.5), the set accessor is invoked with an argument (whose value is that of the right-hand side of the assignment or the operand of the ++ or -- operator) that provides the new value (§7.17.1). The body of a set accessor must conform to the rules for void methods described in §10.6.10. In particular, return statements in the set accessor body are not permitted to specify an expression. Since a set accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declaration in a set accessor to have that name.

Based on the presence or absence of the get and set accessors, a property is classified as follows:
