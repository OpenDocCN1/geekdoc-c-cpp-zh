You’ll learn more about properties in subsequent chapters. Actually, the get and set keywords used in declaring property accessors are treated in a context-sensitive manner, too.

Similarly, the value identifier has a specialized meaning in the context of indexers and events. Thanks to this contextual treatment, the use of value is not reserved elsewhere, so you can just write the following:

```
int value = discount.Value;
```

# ON BACKWARD COMPATIBILITY AND KEYWORD REUSE

Backward compatibility is a big deal to the C# programming language. Every time a new version is released, it’s key to ensure existing code keeps compiling fine. Contextual keywords are one way to ensure this. When new keywords are required to raise the expressiveness of the language required for new language features, they’re made into keywords only in certain contexts.

Even though C# 1.0 didn’t have compatibility issues to worry about, contextual keywords were used to reduce the number of reserved words that are commonly used in English lingo, such as value, get, and set. In C# 2.0, new contextual keywords were added (for example, the where keyword used for generic constraints).

Going even further with this, certain keywords are reused in different contexts where they have a different meaning. This might sound confusing, but actually it’s not that bad. For example, given that the where keyword was already used in C# 2.0 and version 3 wanted to add query comprehension syntax, what would be the obvious choice to express a filter? Right, where strikes again.

# Syntax Highlighting in Visual Studio

Keywords, including ones that have a contextual characteristic, are highlighted in the Visual Studio code editor. Assuming a default color scheme, sequences of characters that have a special meaning in a given context are blue.

For Figure 4.4, I’ve changed the default setting to make keywords appear bold. Settings to control the code editor’s look and feel can be found under Tools, Options, Environment, Fonts and Colors. Select Keyword under Display items to control this setting for (contextual) keywords. Notice how the background compiler for C# recognizes the contextual use of the value keyword, asking the code editor to format it appropriately only in that particular context.