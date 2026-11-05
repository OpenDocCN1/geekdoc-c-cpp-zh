+   - How an implementation enforces the restrictions on the allowable *Unicode_Escape_Sequence* values is an implementation issue.

end note

Example: Examples of valid identifiers are identifier1, _identifier2, and @if. end example

An identifier in a conforming program shall be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15. The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.

The prefix "@" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages. The character @ is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix. An identifier with an @ prefix is called a verbatim identifier.

Note: Use of the @ prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style. end note

Example: The example:

```
class @class
{
    public static void @static(bool @bool)
    {
        if (@bool)
        {
            System.Console.WriteLine("true");
        }
        else
        {
            System.Console.WriteLine("false");
        }
    }
}

class Class1
{
    static void M()
    {
        c1\u0061ss.st\u0061tic(true);
    }
}
```

defines a class named "class" with a static method named "static" that takes a parameter named "bool". Note that since Unicode escapes are not permitted in keywords, the token "c1\u0061ss" is an identifier, and is the same identifier as "@class".

end example

Two identifiers are considered the same if they are identical after the following transformations are applied, in order:

+   - The prefix "@", if used, is removed.
+   - Each *Unicode_Escape_Sequence* is transformed into its corresponding Unicode character.
+   - Any *Formatting_Characters* are removed.