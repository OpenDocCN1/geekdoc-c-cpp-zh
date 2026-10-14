Consider defining a struct instead of a class if instances of the type are small and commonly short-lived or are commonly embedded in other objects.

This doesn’t seem unreasonable if we take it at face value. In particular, the rationale behind value types being small is directly related to memory usage and copy-by-value behavior: structs that have many fields take up more memory space, and the cost of copying a value from one location to another is correspondingly higher.

However, this advice is focused purely on memory use and performance implications, and it’s silent on when we should use records or record structs. Other semantic differences between value types and other types exist that we should take into account. While recommendations like this can guide us, they tell only a small part of the story. Every application will have its own requirements, constraints, and behavior. We don’t have one single rule to apply that will be appropriate universally.

Policies that insist, or at least suggest, that value types have few data members and be short-lived focus on the technical mechanisms of memory representation and use, rather than the more conceptual premise of what behavior the type should exhibit. Values might often be small, but that doesn’t mean that all small types should be structs. A reference type might have only a single field, but that doesn’t automatically indicate that it should be a struct or other value-like type.

Correspondingly, just because we require a type that has several fields doesn’t mean that it can’t be a value type. If value semantics make sense for our type, we should make it a value type, regardless of how much data it carries with it. The number of fields required by an object shouldn’t be the main factor in our decision-making. If we’re worried about the cost of copying large values, we might endow a reference type with value-like behavior to address those concerns, a topic we’ll revisit in Chapter 8.

One way we can determine where we might use value types is to compare their characteristics with other types in a program. Although we can’t consider every possible object type for any potential application, some common categories of object roles are shared by many programs, as we’ll discuss next.

# Object Relationships

Object-oriented applications comprise a variety of objects with different roles, responsibilities, and interactions. These roles are characterized by the relationships between objects and how those objects collaborate to form a coherent application.

When we’re designing an application, it’s easy to overlook the central role played by values and value types. If we recognize their importance, we can often simplify our designs and make our programs clearer and easier to reason about.

We might think of a value as simply the payload of a variable, whether that’s the representation of an int or the properties of an object on the heap. It’s tempting to view the values we use as incidental to an application’s