
## PART III

## Essential Types

- CHAPTER 14 Chars, Strings, and Working with Text ...... 317
- CHAPTER 15 Enumerated Types and Bit Flags .......... 361
- CHAPTER 16 Arrays ................................. 373
- CHAPTER 17 Delegates .............................. 391
- CHAPTER 18 Custom Attributes ...................... 421
- CHAPTER 19 Nullable Value Types ................... 441

To ease development, the Char type also offers several static methods, such as IsDigit, IsLetter, IsWhiteSpace, IsUpper, IsLower, IsPunctuation, IsLetterOrDigit, IsControl, IsNumber, IsSeparator, IsSurrogate, IsLowSurrogate, IsHighSurrogate, and IsSymbol. Most of these methods call GetUnicodeCategory internally and simply return true or false accordingly. Note that all of these methods take either a single character for a parameter or a String and the index of a character within the String as parameters.

In addition, you can convert a single character to its lowercase or uppercase equivalent in a culture-agnostic way by calling the static ToLowerInvariant or ToUpperInvariant method. Alternatively, the ToLower and ToUpper methods convert the character by using the culture information associated with the calling thread (which the methods obtain internally by querying the static CurrentCulture property of the System.Globalization.CultureInfo class). You can also specify a particular culture by passing an instance of the CultureInfo class to these methods. ToLower and ToUpper require culture information because letter casing is a culture-dependent operation. For example, Turkish considers the uppercase of U+0069 (LATIN SMALL LETTER I) to be U+0130 (LATIN CAPITAL LETTER I WITH DOT ABOVE), whereas other cultures consider the result to be U+0049 (LATIN CAPITAL LETTER I).

Besides these static methods, the Char type also offers a few instance methods of its own. The Equals method returns true if two Char instances represent the same 16-bit Unicode code point. The CompareTo methods (defined by the IComparable/IComparable<Char> interfaces) return a comparison of two Char instances; this comparison is not culture-sensitive. The ConvertFromUtf32 method produces a string consisting of one or two UTF-16 characters from a single UTF-32 character. The ConvertToUtf32 method produces a UTF-32 character from a low/high surrogate pair or from a string. The ToString method returns a String consisting of a single character. The opposite of ToString is Parse/TryParse, which takes a single-character String and returns its UTF-16 code point.

The last method, GetNumericValue, returns the numeric equivalent of a character. I demonstrate this method in the following code.

```csharp
using System;

public static class Program {
    public static void Main() {
        Double d;
        d = Char.GetNumericValue('\u0033');   // '\u0033' is the "digit 3"
        Console.WriteLine(d.ToString());      // Displays "3"

        // '\u00bc' is the "vulgar fraction one quarter ('¼')"
        d = Char.GetNumericValue('\u00bc');
        Console.WriteLine(d.ToString());      // Displays "0.25"

        // 'A' is the "latin capital letter A"
        d = Char.GetNumericValue('A');
        Console.WriteLine(d.ToString());      // Displays "-1"
    }
}
```

Finally, three techniques allow you to convert between various numeric types and Char instances and vice versa. The techniques are listed here in order of preference:

- **Casting** The easiest way to convert a Char to a numeric value such as an Int32 is simply by casting. Of the three techniques, this is the most efficient because the compiler emits Intermediate Language (IL) instructions to perform the conversion, and no methods have to be called. In addition, some languages (such as C#) allow you to indicate whether the conversion should be performed using checked or unchecked code (discussed in Chapter 5, "Primitive, Reference, and Value Types").
- **Use the Convert type** The System.Convert type offers several static methods that are capable of converting a Char to a numeric type and vice versa. All of these methods perform the conversion as a checked operation, causing an OverflowException to be thrown if the conversion results in the loss of data.
- **Use the IConvertible interface** The Char type and all of the numeric types in the .NET Framework Class Library (FCL) implement the IConvertible interface. This interface defines methods such as ToUInt16 and ToChar. This technique is the least efficient of the three because calling an interface method on a value type requires that the instance be boxed—Char and all of the numeric types are value types. The methods of IConvertible throw a System.InvalidCastException if the type can't be converted (such as converting a Char to a Boolean) or if the conversion results in a loss of data. Note that many types (including the FCL's Char and numeric types) implement IConvertible's methods as explicit interface member implementations (described in Chapter 13, "Interfaces"). This means that you must explicitly cast the instance to an IConvertible before you can call any of the interface's methods. All of the methods of IConvertible except GetTypeCode accept a reference to an object that implements the IFormatProvider interface. This parameter is useful if for some reason the conversion needs to take culture information into account. For most conversions, you can pass null for this parameter because it would be ignored anyway.

The following code demonstrates how to use these three techniques.

```csharp
using System;

public static class Program {
    public static void Main() {
        Char c;
        Int32 n;

        // Convert number <-> character using C# casting
        c = (Char) 65;
        Console.WriteLine(c);              // Displays "A"

        n = (Int32) c;
        Console.WriteLine(n);              // Displays "65"

        c = unchecked((Char) (65536 + 65));
        Console.WriteLine(c);              // Displays "A"

        // Convert number <-> character using Convert
        c = Convert.ToChar(65);              // Displays "A"
        Console.WriteLine(c);

        n = Convert.ToInt32(c);              // Displays "65"
        Console.WriteLine(n);


        // This demonstrates Convert's range checking
        try {
            c = Convert.ToChar(70000);       // Too big for 16 bits
            Console.WriteLine(c);            // Doesn't execute
        }
        catch (OverflowException) {
            Console.WriteLine("Can't convert 70000 to a Char.");
        }


        // Convert number <-> character using IConvertible
        c = ((IConvertible) 65).ToChar(null);
        Console.WriteLine(c);                // Displays "A"

        n = ((IConvertible) c).ToInt32(null);
        Console.WriteLine(n);                // Displays "65"
    }
}
```

## The System.String Type

One of the most used types in any application is System.String. A String represents an immutable sequence of characters. The String type is derived immediately from Object, making it a reference type, and therefore, String objects (its array of characters) always live in the heap, never on a thread's stack. The String type also implements several interfaces (IComparable/IComparable<String>, ICloneable, IConvertible, IEnumerable/IEnumerable<Char>, and IEquatable<String>).

### Constructing Strings

Many programming languages (including C#) consider String to be a primitive type—that is, the compiler lets you express literal strings directly in your source code. The compiler places these literal strings in the module's metadata, and they are then loaded and referenced at run time.

In C#, you can't use the new operator to construct a String object from a literal string.

```csharp
using System;

public static class Program {
    public static void Main() {
        String s = new String("Hi there.");  // <-- Error
        Console.WriteLine(s);
    }
}
```
