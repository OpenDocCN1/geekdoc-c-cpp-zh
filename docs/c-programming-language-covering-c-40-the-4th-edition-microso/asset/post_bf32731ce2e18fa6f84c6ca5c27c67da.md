
## A. Documentation Comments

```csharp
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>True if the points have the same location and they have
/// the exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator!="/>
public static bool operator ==(Point p1, Point p2)
{
    if ((object)p1 == null || (object)p2 == null)
    {
        return false;
    }
    if (p1.GetType() == p2.GetType())
    {
        return (p1.X == p2.X) && (p1.Y == p2.Y);
    }
    return false;
}
/// <summary>This operator determines whether two points have the same
/// location.</summary>
/// <param name="p1"><c>p1</c> is the first point to be compared.</param>
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>True if the points do not have the same location and the
/// exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator=="/>
public static bool operator !=(Point p1, Point p2)
{
    return !(p1 == p2);
}
/// <summary>This is the entry point of the Point class testing
/// program.</summary>
/// <para>This program tests each method and operator, and
/// is intended to be run after any nontrivial maintenance has
/// been performed on the Point class.</para>
public static void Main()
{
    // Class test code goes here
}
```

### A.4.2 Resulting XML

Here is the output produced by one documentation generator when given the source code for class Point, shown above:

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
<members>
  <member name="T:Graphics.Point">
    <summary>
      Class <c>Point</c> models a point in a two-dimensional
      plane.
    </summary>
  </member>
  <member name="F:Graphics.Point.x">
    <summary>
      Instance variable <c>x</c> represents the point's
      x-coordinate.
    </summary>
  </member>
  <member name="F:Graphics.Point.y">
    <summary>
      Instance variable <c>y</c> represents the point's
      y-coordinate.
    </summary>
  </member>
  <member name="M:Graphics.Point.#ctor">
    <summary>
      This constructor initializes the new point to
      (0,0).
    </summary>
  </member>
  <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
    <summary>
      This constructor initializes the new point to
      (<paramref name="x"/>, <paramref name="y"/>).
    </summary>
    <param>
      <c>x</c> is the new point's x-coordinate.
    </param>
    <param>
      <c>y</c> is the new point's y-coordinate.
    </param>
  </member>
  <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
    <summary>
      This method changes the point's location to
      the given coordinates.
    </summary>
    <param>
      <c>x</c> is the new x-coordinate.
    </param>
    <param>
      <c>y</c> is the new y-coordinate.
    </param>
    <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
  </member>
<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>
This method changes the point's location by
the given x- and y-offsets.
<example>
For example:
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
results in <c>p</c>'s having the value (2,8).
</example>
</summary>
<param name="x">
<c>x</c> is the relative x-offset.
</param>
<param name="y">
<c>y</c> is the relative y-offset.
</param>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
<summary>
This method determines whether two points have the same
location.
</summary>
<param name="obj">
<c>obj</c> is the object to be compared to the current
object.
</param>
<returns>
True if the points have the same location and they have
the exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</seealso>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
<summary>Report a point's location as a string.</summary>
<returns>
A string representing a point's location, in the form
(x,y)
without any leading, trailing, or embedded whitespace.
</returns>
</member>
<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
<summary>
This operator determines whether two points have the
same
location.
</summary>
</summary>
<param>
  <c>p1</c> is the first point to be compared.
</param>
<param>
  <c>p2</c> is the second point to be compared.
</param>
<returns>
  True if the points have the same location and they have
  the exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
  <summary>
    This operator determines whether two points have the
    same
    location.
  </summary>
  <param>
    <c>p1</c> is the first point to be compared.
  </param>
  <param>
    <c>p2</c> is the second point to be compared.
  </param>
  <returns>
    True if the points do not have the same location and the
    exact same type; otherwise, false.
  </returns>
  <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
  <seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.Main">
  <summary>
    This is the entry point of the Point class testing
    program.
    <para>
      This program tests each method and operator, and
      is intended to be run after any nontrivial maintenance has
      been performed on the Point class.
    </para>
  </summary>
</member>
<member name="P:Graphics.Point.X">
  <value>
    Property <c>X</c> represents the point's
    x-coordinate.
  </value>
</member>
<member name="P:Graphics.Point.Y">
    <value>
Property <c>Y</c> represents the point's
y-coordinate.
    </value>
</member>
</members>
</doc>
```

## B. Grammar

This appendix contains summaries of the lexical and syntactic grammars found in the main document, and of the grammar extensions for unsafe code. Grammar productions appear here in the same order that they appear in the main document.

### B.1 Lexical Grammar

```
input:
    input-section_opt
input-section:
    input-section-part
    input-section input-section-part
input-section-part:
    input-elements_opt new-line
    pp-directive
input-elements:
    input-element
    input-elements input-element
input-element:
    whitespace
    comment
    token
```

### B.1.1 Line Terminators

new-line:
- Carriage return character (U+000D)
- Line feed character (U+000A)
- Carriage return character (U+000D) followed by line feed character (U+000A)
- Next line character (U+0085)
- Line separator character (U+2028)
- Paragraph separator character (U+2029)

### B.1.2 Comments

```
comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt

input-characters:
  input-character
  input-characters input-character

input-character:
  Any Unicode character except a new-line-character

new-line-character:
  Carriage return character (U+000D)
  Line feed character (U+000A)
  Next line character (U+0085)
  Line separator character (U+2028)
  Paragraph separator character (U+2029)

delimited-comment:
  /* delimited-comment-text_opt asterisks /

delimited-comment-text:
  delimited-comment-section
  delimited-comment-text delimited-comment-section

delimited-comment-section:
  /
  asterisks_opt not-slash-or-asterisk

asterisks:
  *
  asterisks *

not-slash-or-asterisk:
  Any Unicode character except / or *
```

### B.1.3 White Space

```
whitespace:
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

### B.1.4 Tokens

```
token:
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```

### B.1.5 Unicode Character Escape Sequences

```
unicode-escape-sequence:
    \u hex-digit hex-digit hex-digit hex-digit
    \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

### B.1.6 Identifiers

```
identifier:
    available-identifier
    @ identifier-or-keyword
```

```
available-identifier:
    An identifier-or-keyword that is not a keyword
```

```
identifier-or-keyword:
    identifier-start-character identifier-part-characters_opt
```

```
identifier-start-character:
    letter-character
    _ (the underscore character U+005F)
```

```
identifier-part-characters:
    identifier-part-character
    identifier-part-characters identifier-part-character
```
