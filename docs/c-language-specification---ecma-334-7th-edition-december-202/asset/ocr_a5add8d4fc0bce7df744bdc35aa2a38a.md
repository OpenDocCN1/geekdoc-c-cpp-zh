# D.3 Recommended tags

# D.3.1 General

The documentation generator must accept and process any tag that is valid according to the rules of XML. The following tags provide commonly used functionality in user documentation. (Of course, other tags are possible.)

| Tag | Reference | Purpose |
|---|---|---|
| `<c>` | §D.3.2 | Set text in a code-like font |
| `<code>` | §D.3.3 | Set one or more lines of source code or program output |
| `<example>` | §D.3.4 | Indicate an example |
| `<exception>` | §D.3.5 | Identifies the exceptions a method can throw |
| `<include>` | §D.3.6 | Includes XML from an external file |
| `<list>` | §D.3.7 | Create a list or table |
| `<para>` | §D.3.8 | Permit structure to be added to text |
| `<param>` | §D.3.9 | Describe a parameter for a method or constructor |
| `<paramref>` | §D.3.10 | Identify that a word is a parameter name |
| `<permission>` | §D.3.11 | Document the security accessibility of a member |
| `<remarks>` | §D.3.12 | Describe additional information about a type |
| `<returns>` | §D.3.13 | Describe the return value of a method |
| `<see>` | §D.3.14 | Specify a link |
| `<seealso>` | §D.3.15 | Generate a See Also entry |
| `<summary>` | §D.3.16 | Describe a type or a member of a type |
| `<typeparam>` | §D.3.17 | Describe a type parameter for a generic type or method |
| `<typeparamref>` | §D.3.18 | Identify that a word is a type parameter name |
| `<value>` | §D.3.19 | Describe a property |

# D.3.2 <c>

This tag provides a mechanism to indicate that a fragment of text within a description should be set in a special font such as that used for a block of code. For lines of actual code, use <code> (§D.3.3).

**Syntax:**

```
<c>text</c>
```

**Example:**

```
/// <summary>
/// Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
}
```