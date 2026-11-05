# C# LANGUAGE SPECIFICATION

```
indexer-declaration:
    attributes_opt indexer-modifiers_opt indexer-declarator { accessor-declarations }
indexer-modifiers:
    indexer-modifier
    indexer-modifiers indexer-modifier
indexer-modifier:
    new
    public
    protected
    internal
    private
    virtual
    sealed
    override
    abstract
    extern
indexer-declarator:
    type this [ formal-parameter-list ]
    type interface-type . this [ formal-parameter-list ]
```

An indexer-declaration may include a set of attributes (§17) and a valid combination of the four access modifiers (§10.3.5), the new (§10.3.4), virtual (§10.6.3), override (§10.6.4), sealed (§10.6.5), abstract (§10.6.6), and extern (§10.6.7) modifiers.

Indexer declarations are subject to the same rules as method declarations (§10.6) with regard to valid combinations of modifiers, with the one exception being that the static modifier is not permitted on an indexer declaration.

The modifiers virtual, override, and abstract are mutually exclusive except in one case. The abstract and override modifiers may be used together so that an abstract indexer can override a virtual one.

The type of an indexer declaration specifies the element type of the indexer introduced by the declaration. Unless the indexer is an explicit interface member implementation, the type is followed by the keyword this. For an explicit interface member implementation, the type is followed by an interface-type, a '.', and the keyword this. Unlike other members, indexers do not have user-defined names.

The formal-parameter-list specifies the parameters of the indexer. The formal parameter list of an indexer corresponds to that of a method (§10.6.1), except that at least one parameter must be specified, and that the ref and out parameter modifiers are not permitted.

The type of an indexer and each of the types referenced in the formal-parameter-list must be at least as accessible as the indexer itself (§3.5.4).

The accessor-declarations (§10.7.2), which must be enclosed in '{' and '}' tokens, declare the accessors of the indexer. The accessors specify the executable statements associated with reading and writing indexer elements.

Even though the syntax for accessing an indexer element is the same as that for an array element, an indexer element is not classified as a variable. Thus, it is not possible to pass an indexer element as a ref or out argument.