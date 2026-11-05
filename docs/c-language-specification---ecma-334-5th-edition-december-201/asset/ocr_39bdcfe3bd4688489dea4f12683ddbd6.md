```
```xml
<item>
  <term>term</term>
  <description>description</description>
</item>
</list>
```
```

where

*term*

The term to define, whose definition is in *description*.

*description*

Either an item in a bullet or numbered list, or the definition of a *term*.

# Example:

```
```csharp
public class MyClass
{
/// <summary>Here is an example of a bulleted list:
/// <list type="bullet">
/// <item>
/// <description>Item 1.</description>
/// </item>
/// <item>
/// <description>Item 2.</description>
/// </item>
/// </list>
/// </summary>
public static void Main () {
    // ...
}
```
```

# D.3.8 `<para>`

This tag is for use inside other tags, such as `<summary>` (§D.3.16) or `<returns>` (§D.3.13), and permits structure to be added to text.

# Syntax:

```
```xml
<para>content</para>
```
```

where

*content*

The text of the paragraph.

# Example:

```
```csharp
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```
```

# D.3.9 `<param>`

This tag is used to describe a parameter for a method, constructor, or indexer.

# Syntax:

```
```xml
<param name="name">description</param>
```
```

where

*name*

The name of the parameter.