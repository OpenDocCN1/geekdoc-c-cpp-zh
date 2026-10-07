# Attributes

writes out the strings for each enumeration flag that is set. In Listing 18.23, file .Attributes.ToString() returns "ReadOnly, "Hidden" rather than the 3 it would have returned without the FlagsAttribute flag. if two enumeration values are the same, the ToString() call would return the first one. As mentioned earlier, however, you should use caution when relying on this outcome because it is not localizable.

Parsing a value from a string to the enumeration also works, provided that each enumeration value identifier is separated by a comma.

Note that FlagsAttribute does not automatically assign the unique flag values or check that flags have unique values. The values of each enumeration item must still be assigned explicitly.

# Predefined Attributes

The AttributeUsageAttribute attribute has a special characteristic that you haven't seen yet in the custom attributes you have created in this book. This attribute affects the behavior of the compiler, causing it to sometimes return an error. Unlike the reflection code that you wrote earlier for retrieving CommandRequiredAttribute CommandLineSwitchAliasAttribute, AttributeUsageAttribute has no runtime code; instead, it has built-in compiler support.

AttributeUsageAttribute is a predefined attribute. Not only do such attributes provide additional metadata about the constructs they decorate, but the runtime and compiler also behave differently to facilitate these' functionality. Attributes such as AttributeUsageAttribute, FlagsAttribute, ObsoleteAttribute, and ConditionalAttribute are examples of predefined attributes. They implement special behavior that only the CLI provider or compiler can offer there are no extension points for additional noncustom attributes. In contrast, custom attributes are entirely passive. Listing 18.23 includes a couple of predefined attributes; Chapter 19 includes a few more.