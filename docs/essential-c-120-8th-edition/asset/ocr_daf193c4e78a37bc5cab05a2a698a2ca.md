# Chapter 18: Reflection, Attributes, and Dynamic Programming

# nameof Operator

We briefly touched on the nameof operator in Chapter 11, where it was used to provide the name of a parameter in an argument exception:

```
throw new ArgumentException(
  "The argument did not represent a digit", nameof(textDigit));
```

This contextual keyword³ produces a constant string containing the unqualified name of whatever program element is specified as an argument. In this case, textDigit is a parameter to the method, so nameof(textDigit) returns “textDigit.” (Given that this activity happens at compile time, nameof is not technically reflection. We include it here because ultimately it retrieves data about the assembly and its structure).

You might ask what advantage is gained by using nameof(textDigit) over simply "textDigit" (especially given that the latter might seem easier to use to some programmers). The advantages are twofold:

+   - The C# compiler ensures that the argument to the nameof operator is, in fact, a valid program element. This prevents errors when a program element is changed, helps prevent misspellings, and so on.

+   - IDE tools work better with the nameof operator than with literal strings. For example, the “find all references” tool will find program elements mentioned in a nameof expression but not in a literal string. The automatic refactoring works better, and so on.

In the snippet given earlier, nameof(textDigit) produces the name of a parameter. In reality, the nameof operator works with any program element that is in scope. In fact, starting in C# 11, you can even use nameof with parameter names of the method an attribute is decorating. For example, Listing 18.7 uses nameof to pass the property name to INotifyPropertyChanged.PropertyChanged.

+   - Introduced in C# 6.0.