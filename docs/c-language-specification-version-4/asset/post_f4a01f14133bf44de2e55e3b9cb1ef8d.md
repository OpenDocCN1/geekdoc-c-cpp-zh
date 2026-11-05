
The text within documentation comments must be well formed according to the rules of XML (http://www.w3.org/TR/REC-xml). If the XML is ill formed, a warning is generated and the documentation file will contain a comment saying that an error was encountered.

Although developers are free to create their own set of tags, a recommended set is defined in §A.2. Some of the recommended tags have special meanings:

- The `<param>` tag is used to describe parameters. If such a tag is used, the documentation generator must verify that the specified parameter exists and that all parameters are described in documentation comments. If such verification fails, the documentation generator issues a warning.
- The `cref` attribute can be attached to any tag to provide a reference to a code element. The documentation generator must verify that this code element exists. If the verification fails, the documentation generator issues a warning. When looking for a name described in a `cref` attribute, the documentation generator must respect namespace visibility according to `using` statements appearing within the source code. For code elements that are generic, the normal generic syntax (ie “`List<T>`”) cannot be used because it produces invalid XML. Braces can be used instead of brackets (ie “`List{T}`”), or the XML escape syntax can be used (ie “`List&lt;T&gt;`”).
- The `<summary>` tag is intended to be used by a documentation viewer to display additional information about a type or member.
- The `<include>` tag includes information from an external XML file.

Note carefully that the documentation file does not provide full information about the type and members (for example, it does not contain any type information). To get such information about a type or member, the documentation file must be used in conjunction with reflection on the actual type or member.

## A.2 Recommended tags

The documentation generator must accept and process any tag that is valid according to the rules of XML. The following tags provide commonly used functionality in user documentation. (Of course, other tags are possible.)

| Tag | Section | Purpose |
|---|---|---|
| <c> | A.2.1 | Set text in a code-like font |
| <code> | A.2.2 | Set one or more lines of source code or program output |
| <example> | A.2.3 | Indicate an example |
| <exception> | A.2.4 | Identifies the exceptions a method can throw |
| <include> | A.2.5 | Includes XML from an external file |
| <list> | A.2.6 | Create a list or table |
| <para> | A.2.7 | Permit structure to be added to text |
| <param> | A.2.8 | Describe a parameter for a method or constructor |
| <paramref> | A.2.9 | Identify that a word is a parameter name |
| <permission> | A.2.10 | Document the security accessibility of a member |
| <remark> | A.2.11 | Describe additional information about a type |
| <returns> | A.2.12 | Describe the return value of a method |
| <see> | A.2.13 | Specify a link |
| <seealso> | A.2.14 | Generate a See Also entry |
| <summary> | A.2.15 | Describe a type or a member of a type |
| <value> | A.2.16 | Describe a property |
| <typeparam> |  | Describe a generic type parameter |
| <typeparamref> |  | Identify that a word is a type parameter name |

### A.2.1 <c>

This tag provides a mechanism to indicate that a fragment of text within a description should be set in a special font such as that used for a block of code. For lines of actual code, use <code> (§A.2.2).

**Syntax:**

```
<c>text</c>
```

**Example:**

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
public class Point
{
    // ...
}
```

### A.2.2 <code>

This tag is used to set one or more lines of source code or program output in some special font. For small code fragments in narrative, use <c> (§A.2.1).

**Syntax:**

```
<code>source code or program output</code>
```

**Example:**

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### A.2.3 <example>

This tag allows example code within a comment, to specify how a method or other library member may be used. Ordinarily, this would also involve use of the tag <code> (§A.2.2) as well.

**Syntax:**

```
<example>description</example>
```

**Example:**

See <code> (§A.2.2) for an example.

### A.2.4 <exception>

This tag provides a way to document the exceptions a method can throw.

**Syntax:**

```
<exception cref="member">description</exception>
```

**where**

**cref="member"**

The name of a member. The documentation generator checks that the given member exists and translates member to the canonical element name in the documentation file.

**description**

A description of the circumstances in which the exception is thrown.

**Example:**

```
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        // ...
    }
}
```

### A.2.5 <include>

This tag allows including information from an XML document that is external to the source code file. The external file must be a well-formed XML document, and an XPath expression is applied to that document to specify what XML from that document to include. The <include> tag is then replaced with the selected XML from the external document.

**Syntax:**

```
<include file="filename" path="xpath" />
```

**where**

**file="filename"**

The file name of an external XML file. The file name is interpreted relative to the file that contains the include tag.

**path="xpath"**

An XPath expression that selects some of the XML in the external XML file.

**Example:**

If the source code contained a declaration like:

```
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

and the external file "docs.xml" had the following contents:

```
<?xml version="1.0"?>
<extradoc>
  <class name="IntList">
    <summary>
      Contains a list of integers.
    </summary>
  </class>
  <class name="StringList">
    <summary>
      Contains a list of integers.
    </summary>
  </class>
</extradoc>
```

then the same documentation is output as if the source code contained:

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### A.2.6 <list>

This tag is used to create a list or table of items. It may contain a <listheader> block to define the heading row of either a table or definition list. (When defining a table, only an entry for term in the heading need be supplied.)

Each item in the list is specified with an <item> block. When creating a definition list, both term and description must be specified. However, for a table, bulleted list, or numbered list, only description need be specified.

**Syntax:**

```
<list type="bullet" | "number" | "table">
  <listheader>
    <term>term</term>
    <description>description</description>
  </listheader>
  <item>
    <term>term</term>
    <description>description</description>
  </item>
  ...item
  <term>term</term>
  <description>description</description>
  </item>
</list>
```

**where**

**term**

The term to define, whose definition is in description.

**description**

Either an item in a bullet or numbered list, or the definition of a term.

**Example:**

```
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
}
```

### A.2.7 <para>

This tag is for use inside other tags, such as <summary> (§A.2.11) or <returns> (§A.2.12), and permits structure to be added to text.

**Syntax:**

```
<para>content</para>
```

**where**

**content**

The text of the paragraph.

**Example:**
