for enumeration constant, the (only) declaration of the identifier;

for a typedefed name, which is the first (or only) declaration of the identifier.

6 The declaration specifiers consist of a sequence of specifiers that indicate the linkage, storage duration, and part of the entities that the declarators denote. The init-declarator-list is a comma-separated sequence of declarators, each of which may have type information, or an initializer, or both. The declarators contain the identifiers (if any) being declared.

7 If an identifier for an object is declared with no linkage, the type for the object should be complete by the end of its declarator, or by the end of its init-declarator if it has an initializer; in the case of function parameters (including in prototypes), it is the adjusted type (see 6.7.6.3) that is required to be complete.

**Forward references:** declarators (6.7.6), enumeration specifiers (6.7.2.2), initialization (6.7.9), type names (6.7.7), type qualifiers (6.7.3).

# 6.7.1 Storage-class specifiers

Syntax

```
storage-class-specifier:
typedef
extern
static
_Thread_local
auto
register
```

**Constraints

2 At most, one storage-class specifier may be given in the declaration specifiers in a declaration, except that _Thread_local may appear with **static** or **extern**.¹²⁰

3 In the declaration of an object with block scope, if the declaration specifiers include _Thread_local, they shall also include either **static** or **extern**. If _Thread_local appears in any declaration of an object, it shall be present in every declaration of that object.

4 _Thread_local shall not appear in the declaration specifiers of a function declaration.

> 119) Function definitions have a different syntax, described in 6.9.1.

> 120) See “future language directions” (6.11.5).