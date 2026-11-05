The type of an indexer declaration specifies the element type of the indexer introduced by the declaration. Unless the indexer is an explicit interface member implementation, the type is followed by the keyword this. For an explicit interface member implementation, the type is followed by an interface-type, a ".", and the keyword this. Unlike other members, indexers do not have user-defined names.

The formal-parameter-list specifies the parameters of the indexer. The formal parameter list of an indexer corresponds to that of a method (§15.6.2), except that at least one parameter shall be specified, and that the this, ref, and out parameter modifiers are not permitted.

The type of an indexer and each of the types referenced in the formal-parameter-list shall be at least as accessible as the indexer itself (§8.5.5).

The accessor-declarations (§15.7.3), which shall be enclosed in "{" and "}" tokens, declare the accessors of the indexer. The accessors specify the executable statements associated with reading and writing indexer elements.

Even though the syntax for accessing an indexer element is the same as that for an array element, an indexer element is not classified as a variable. Thus, it is not possible to pass an indexer element as a ref or out argument.

The formal-parameter-list of an indexer defines the signature (§8.6) of the indexer. Specifically, the signature of an indexer consists of the number and types of its formal parameters. The element type and names of the formal parameters are not part of an indexer’s signature.

The signature of an indexer shall differ from the signatures of all other indexers declared in the same class.

Indexers and properties are very similar in concept, but differ in the following ways:

+   - A property is identified by its name, whereas an indexer is identified by its signature.
+   - A property is accessed through a simple-name (§12.7.3) or a member-access (§12.7.5), whereas an indexer element is accessed through an element-access (§12.7.7.3).
+   - A property can be a static member, whereas an indexer is always an instance member.
+   - A get accessor of a property corresponds to a method with no parameters, whereas a get accessor of an indexer corresponds to a method with the same formal parameter list as the indexer.
+   - A set accessor of a property corresponds to a method with a single parameter named value, whereas a set accessor of an indexer corresponds to a method with the same formal parameter list as the indexer, plus an additional parameter named value.
+   - It is a compile-time error for an indexer accessor to declare a local variable or local constant with the same name as an indexer parameter.
+   - In an overriding property declaration, the inherited property is accessed using the syntax base.P, where P is the property name. In an overriding indexer declaration, the inherited indexer is accessed using the syntax base[E], where E is a comma-separated list of expressions.

Aside from these differences, all rules defined in §15.7.3 and §15.7.6 apply to indexer accessors as well as to property accessors.

When an indexer declaration includes an extern modifier, the indexer is said to be an external indexer. Because an external indexer declaration provides no actual implementation, each of its accessor-declarations consists of a semicolon.

[Example: The example below declares a BitArray class that implements an indexer for accessing the individual bits in the bit array.

```
using System;
class BitArray
{
    int[] bits;
    int length;
```