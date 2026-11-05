```
: '/**' Delimited_Comment_Section* ASTERISK+ '/'
;
```

In a Single_Line_Doc_Comment, if there is a Whitespace character following the /// characters on each of the Single_Line_Doc_Comments adjacent to the current Single_Line_Doc_Comment, then that Whitespace character is not included in the XML output.

In a Delimited_Doc_Comment, if the first non-Whitespace character on the second line is an ASTERISK and the same pattern of optional Whitespace characters and an ASTERISK character is repeated at the beginning of each of the lines within the Delimited_Doc_Comment, then the characters of the repeated pattern are not included in the XML output. The pattern can include Whitespace characters after, as well as before, the ASTERISK character.

# Example:

```
```
/// <summary>
/// Class <>Point</> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
    /// <summary>
    /// Method <>Draw</> renders the point.
    /// </summary>
    void Draw() {...}
}
```
```

The text within documentation comments must be well formed according to the rules of XML (http://www.w3.org/TR/REC-xml). If the XML is ill formed, a warning is generated and the documentation file will contain a comment saying that an error was encountered.

Although developers are free to create their own set of tags, a recommended set is defined in §D.3. Some of the recommended tags have special meanings:

+   - The <param> tag is used to describe parameters. If such a tag is used, the documentation generator must verify that the specified parameter exists and that all parameters are described in documentation comments. If such verification fails, the documentation generator issues a warning.
+   - The <cref> attribute can be attached to any tag to provide a reference to a code element. The documentation generator must verify that this code element exists. If the verification fails, the documentation generator issues a warning. When looking for a name described in a <cref> attribute, the documentation generator must respect namespace visibility according to using statements appearing within the source code. For code elements that are generic, the normal generic syntax (e.g., “List<T>”) cannot be used because it produces invalid XML. Braces can be used instead of brackets (e.g., “List{T}”), or the XML escape syntax can be used (e.g., “List&lt;T&gt;”).
+   - The <summary> tag is intended to be used by a documentation viewer to display additional information about a type or member.
+   - The <include> tag includes information from an external XML file.

Note carefully that the documentation file does not provide full information about the type and members (for example, it does not contain any type information). To get such information about a type or member, the documentation file must be used in conjunction with reflection on the type or member.