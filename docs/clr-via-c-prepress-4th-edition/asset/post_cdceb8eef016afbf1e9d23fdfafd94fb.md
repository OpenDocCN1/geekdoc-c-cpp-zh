
On the other hand, if M had been declared like this:

```csharp
private static Int32 M(IComparable t) {
    ...
}
```

then in order to pass x to M, x would have to be boxed.

For interface constraints, the C# compiler emits certain Intermediate Language (IL) instructions that result in calling the interface method on the value type directly without boxing it. Aside from using interface constraints, there is no other way to get the C# compiler to emit these IL instructions, and therefore, calling an interface method on a value type always causes boxing.

### Implementing Multiple Interfaces That Have the Same Method Name and Signature

Occasionally, you might find yourself defining a type that implements multiple interfaces that define methods with the same name and signature. For example, imagine that there are two interfaces defined as follows:

```csharp
public interface IWindow {
    Object GetMenu();
}
```

```csharp
public interface IRestaurant {
    Object GetMenu();
}
```

Let’s say that you want to define a type that implements both of these interfaces. You’d have to implement the type’s members by using explicit interface method implementations as follows:

```csharp
// This type is derived from System.Object and
// implements the IWindow and IRestaurant interfaces.
public sealed class MarioPizzeria : IWindow, IRestaurant {

    // This is the implementation for IWindow's GetMenu method.
    Object IWindow.GetMenu() { ... }

    // This is the implementation for IRestaurant's GetMenu method.
    Object IRestaurant.GetMenu() { ... }

    // This (optional method) is a GetMenu method that has nothing
    // to do with either interface.
    public Object GetMenu() { ... }
}
```

Because this type must implement multiple and separate GetMenu methods, you need to tell the C# compiler which GetMenu method contains the implementation for a particular interface.

implements, which the various control classes simply inherit to function correctly.

By contrast, Microsoft designed the FCL collections to be interface based. The System.Collections.Generic namespace defines several collection-related interfaces: IEnumerable<out T>, ICollection<T>, IList<T>, and IDictionary<TKey, TValue>. Then Microsoft provided a number of classes, such as List<T>, Dictionary<TKey, TValue>, Queue<T>, Stack<T>, and so on, that implement combinations of these interfaces. Here the designers chose a CAN-DO relationship between the classes and the interfaces because the implementations of these various collection classes are radically different from one another. In other words, there isn't a lot of sharable code between a List<T>, a Dictionary<TKey, TValue>, and a Queue<T>.

The operations these collection classes offer are, nevertheless, pretty consistent. For example, they all maintain a set of elements that can be enumerated, and they all allow adding and removing of elements. If you have a reference to an object whose type implements the IList<T> interface, you can write code to insert elements, remove elements, and search for an element without having to know exactly what type of collection you're working with. This is a very powerful mechanism.

Finally, it should be pointed out that you can actually do both: define an interface and provide a base class that implements the interface. For example, the FCL defines the IComparer<in T> interface and any type can choose to implement this interface. In addition, the FCL provides an abstract base class, Comparer<T>, which implements this interface and provides a default implementation for the non-generic IComparer's Compare method. Having both an interface definition and a base class offers great flexibility because developers can now choose whichever they prefer.

## Chapter 14: Chars, Strings, and Working with Text

In this chapter:

- Characters — 327
- The System.String Type — 330
- Constructing a String Efficiently — 346
- Obtaining a String Representation of an Object: `ToString` — 350
- Parsing a String to Obtain an Object: `Parse` — 359
- Encodings: Converting Between Characters and Bytes — 361
- Secure Strings — 369

In this chapter, I'll explain the mechanics of working with individual characters and strings in the Microsoft .NET Framework. I'll start by talking about the System.Char structure and the various ways that you can manipulate a character. Then I'll go over the more useful System.String class, which allows you to work with immutable strings. (Once created, strings can't be modified in any way.) After examining strings, I'll show you how to perform various operations efficiently to build a string dynamically via the System.Text.StringBuilder class. With the string basics out of the way, I'll then describe how to format objects into strings and how to efficiently persist or transmit strings by using various encodings. Finally, I'll discuss the System.Security.SecureString class, which can be used to protect sensitive string data such as passwords and credit card information.

### Characters

In the .NET Framework, characters are always represented in 16-bit Unicode code values, easing the development of global applications. A character is represented with an instance of the System.Char structure (a value type). The System.Char type is pretty simple. It offers two public read-only constant fields: MinValue, defined as '\0', and MaxValue, defined as '\uffff'.

Given an instance of a Char, you can call the static GetUnicodeCategory method, which returns a value of the System.Globalization.UnicodeCategory enumerated type. This value indicates whether the character is a control character, a currency symbol, a lowercase letter, an uppercase letter, a punctuation character, a math symbol, or another character (as defined by the Unicode standard).

To ease developing, the Char type also offers several static methods, such as IsDigit, IsLetter, IsWhiteSpace, IsUpper, IsLower, IsPunctuation, IsLetterOrDigit, IsControl, IsNumber, IsSeparator, IsSurrogate, IsLowSurrogate, IsHighSurrogate, and IsSymbol. Most of these methods call GetUnicodeCategory internally and simply return true or false accordingly. Note that all of these methods take either a single character for a parameter or a String and the index of a character within the String as parameters.

In addition, you can convert a single character to its lowercase or uppercase equivalent in a culture-agnostic way by calling the static ToLowerInvariant or ToUpperInvariant method. Alternatively, the ToLower and ToUpper methods convert the character by using the culture information associated with the calling thread (which the methods obtain internally by querying the static CurrentCulture property of the System.Globalization.CultureInfo class). You can also specify a particular culture by passing an instance of the CultureInfo class to these methods. ToLower and ToUpper require culture information because letter casing is a culture-dependent operation. For example, Turkish considers the uppercase of U+0069 (LATIN LOWERCASE LETTER I) to be U+0130 (LATIN UPPERCASE LETTER I WITH DOT ABOVE), whereas other cultures consider the result to be U+0049 (LATIN CAPITAL LETTER I).

Besides these static methods, the Char type also offers a few instance methods of its own. The Equals method returns true if two Char instances represent the same 16-bit Unicode code point. The CompareTo methods (defined by the IComparable/IComparable<Char> interfaces) return a comparison of two Char instances; this comparison is not culture-sensitive. The ConvertFromUtf32 method produces a string consisting of one or two UTF-16 characters from a single UTF-32 character. The ConvertToUtf32 produces a UTF-32 character from a low/high surrogate pair or from a string. The ToString method returns a String consisting of a single character. The opposite of ToString is Parse/TryParse, which takes a single-character String and returns its UTF-16 code point.

The last method, GetNumericValue, returns the numeric equivalent of a character. I demonstrate this method in the following code:

```csharp
using System;
```
