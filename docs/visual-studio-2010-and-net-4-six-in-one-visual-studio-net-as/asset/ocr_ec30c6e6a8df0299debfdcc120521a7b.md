The partial method cannot be seen from outside:

```
class Program
{
    static void Main(string[] args)
    {
        CustomTypedCollection c = new CustomTypedCollection();
        c.AddElement(new CustomElement());
    }
}
```

If the Customization.cs file did not contain an implementation part for the BeforeAddingElement partial method, no code would be compiled for this method in Collection.cs.

Of course, partial methods have a few restrictions. For example, they must return void, and are not allowed to have out or ref parameters, nor can they have access modifiers, and they cannot be virtual.

# # SUMMARY

Currently a multi-paradigm programming language, C# began life with version 1.0 in 2002 as a general-purpose, object-oriented language. The development team of the C# language was led by Anders Heijlsberg. The name was inspired from musical notation where a sharp indicates that the note should be made a half step higher in pitch.

The language evolved in parallel with the .NET Framework as the "native" programming language of the framework. New features and changes in the CLR and in the framework's class libraries inspired the language that turned into a real multi-paradigm language supporting not only the original object-oriented programming (OOP) principles, but also declarative, functional, and (with C# 4.0) the dynamic paradigm.

Chapter 24 will familiarize you with the new improvements to the C# language, such as dynamic lookup, named and optional parameters, the new COM-specific features, and variance.