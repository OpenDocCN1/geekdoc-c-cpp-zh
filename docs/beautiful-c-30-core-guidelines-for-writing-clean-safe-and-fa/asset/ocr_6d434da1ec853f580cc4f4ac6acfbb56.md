```
// Element lightweight = H;          // H not
in scope
Element lightweight = Element::H;   // H in
scope
```

While the scope of H is interrupted, you can still reference it by explicitly resolving the scope. This is done by, you guessed it, using ::, the scope resolution operator, and writing Element::H. The scope resolution operator tells the compiler “I mean this one, over here, look!”

Perhaps the name Element is itself in a namespace. Indeed, we would hope that is the case, since declaring anything other than a namespace at global namespace scope is a bad idea. In that case, you direct the compiler to the name Element by resolving its scope, for example, Chemistry::Element::H. You may draw parallels between this and the global Domain Name System, where top-level domains like .com, .net, and country codes resolve the scope; for example google.ie versus google.fr.

In the above example we have yet another overlap of guidelines. Enum.3: “Prefer class enums over “plain” enums” is motivated by the readiness with which enumerators convert to ints, leading to alarming consequences as outlined in the prior chapter. However, preferring enum classes, more properly known as scoped enumerations, will minimize the scope of an enumeration to its definition. It will keep the scope small. This is particularly advantageous for single-character identifiers, like H for hydrogen.

# Template parameter scope

For completeness, we shall review template parameter scope. The scope of a template parameter name begins at the point of declaration and ends at the end of the smallest template declaration in which it was introduced. For example:

Click here to view code image