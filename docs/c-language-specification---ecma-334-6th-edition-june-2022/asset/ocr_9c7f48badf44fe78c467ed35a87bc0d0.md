```
/// Thrown when the master file is corrupted.
/// </exception>
/// <exception cref="MasterFileLockedOpenException">
/// Thrown when the master file is already open.
/// </exception>
public static void ReadRecord(int flag)
{
    if (flag == 1)
    {
        throw new MasterFileFormatCorruptException();
    }
    else if (flag == 2)
    {
        throw new MasterFileLockedOpenException();
    }
    // ...
}
```

# D.3.6 <include>

This tag allows including information from an XML document that is external to the source code file. The external file must be a well-formed XML document, and an XPath expression is applied to that document to specify what XML from that document to include. The <include> tag is then replaced with the selected XML from the external document.

Syntax:

```
<include file="filename" path="xpath" />
```

where

+   - file="filename" is the file name of an external XML file. The file name is interpreted relative to the file that contains the include tag.
+   - path="xpath" is an XPath expression that selects some of the XML in the external XML file.

Example:

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
            Contains a list of strings.
        </summary>
    </class>
</extradoc>
```