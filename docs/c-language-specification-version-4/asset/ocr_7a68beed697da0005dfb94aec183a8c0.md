The attributes, type, and identifier of an interface property declaration have the same meaning as those of a property declaration in a class (§10.7).

The accessors of an interface property declaration correspond to the accessors of a class property declaration (§10.7.2), except that the accessor body must always be a semicolon. Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.

The type of an interface property must be output-safe if there is a get accessor, and must be input-safe if there is a set accessor.

# 13.2.3 Interface events

Interface events are declared using interface-event-declarations:

```
interface-event-declaration:
    attributes_opt new_opt event type identifier ;
```

The attributes, type, and identifier of an interface event declaration have the same meaning as those of an event declaration in a class (§10.8).

The type of an interface event must be input-safe.

# 13.2.4 Interface indexers

Interface indexers are declared using interface-indexer-declarations:

```
interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }
```

The attributes, type, and formal-parameter-list of an interface indexer declaration have the same meaning as those of an indexer declaration in a class (§10.9).

The accessors of an interface indexer declaration correspond to the accessors of a class indexer declaration (§10.9), except that the accessor body must always be a semicolon. Thus, the accessors simply indicate whether the indexer is read-write, read-only, or write-only.

# 13.2.5 Interface member access

Interface members are accessed through member access (§7.6.4) and indexer access (§7.6.6.2) expressions of the form I.M and I[A], where I is an interface type, M is a method, property, or event of that interface type, and A is an indexer argument list.

For interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effects of the member lookup (§7.4), method invocation (§7.6.5.1), and indexer access (§7.6.6.2) rules are exactly the same as for classes and structs: More derived members hide less derived members with the same name or signature. However, for multiple-inheritance interfaces, ambiguities can occur when two or more unrelated base interfaces declare members with the same name or signature. This section shows several examples of such situations. In all cases, explicit casts can be used to resolve the ambiguities.

In the example

```
interface IList
{
    int Count { get; set; }
}
```