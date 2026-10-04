```
internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;

    public Rectangle() {
    }
}
```

When a new Rectangle is constructed, what do you think the m_x and m_y fields in the two Point fields, m_topLeft and m_bottomRight, would be initialized to: 0 or 5? (Hint: This is a question).

Many developers (especially those with a C++ background) would expect the C# compiler to emit code in Rectangle's constructor that automatically calls Point's default parameterless constructor for the Rectangle's two fields. However, to improve the run-time performance of the application, the C# compiler doesn't automatically emit this code. In fact, many compilers will never emit code to call a value type's default constructor even if the value type offers a parameterless constructor. To have a value type's parameterless constructor, the developer must add explicit code to call a value type's constructor.

Based on the information in the preceding paragraph, you should expect the m_x and m_y fields in Rectangle's two Point fields to be initialized to 0 or 1 in the code showed earlier because there are no explicit calls to Point's constructor anywhere in the code.

I had it say that my original question was a trick question. The trick part is that C# doesn't allow a value type to define a parameterless constructor. The previous code wasn't actually compile. The C# compiler produces the following message when attempting to compile: code error CS0568: Structs cannot contain parameterless constructors.

C# purposely disallows value types from defining parameterless constructors to remove any confusion a developer might have when that constructor gets called. If the constructor can't be defined, the compiler can never generate code to call it automatically. Without a parameterless constructor, a value type's fields are always initialized to 0/null.

> Note Strictly speaking, value types are guaranteed to be the 0/null when the value type is a field nested within a reference type. However, stack-based value types are not guaranteed to be 0/null. For verification, any stack-based value type field prior to writing to the field, a security breach is possible. C# and other compilers that read value code would produce verifiable code ensure that all stack-based value types have their fields zeroed out or at least written before being read so that a verification exception won't be thrown at run. For the most part, this means you can assume that your value types have their fields initialized to 0, and you can completely ignore everything in this note.

Keep in mind that although C# doesn't allow value types with parameterless constructors, the CLR does. If the obvious behavior described earlier doesn't bother you, you can use another programming language (such as as IL assembly language) to define your value type with a parameterless constructor.