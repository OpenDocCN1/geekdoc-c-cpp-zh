```
```java
if (attrs.getLength() > 0)
{
    pad(result.append(",\n"), level + 1).append("\"attributes\": ");
    result.append(attributeObject(attrs));
}
NodeList children = elem.getChildNodes();
if (children.getLength() > 0)
{
    pad(result.append(",\n"), level + 1).append("\"children\": [\n");
    for (int i = 0; i < children.getLength(); i++)
    {
        if (i > 0) result.append(",\n");
        result.append(jsonEscape(children.item(i), level + 2));
    }
    result.append("\n");
    pad(result, level + 1).append("]\n");
}
pad(result, level).append("}");
return result;
}

private static StringBuilder pad(StringBuilder builder, int level)
{
    for (int i = 0; i < level; i++) builder.append("  ");
    return builder;
}

private static StringBuilder attributeObject(NamedNodeMap attrs)
{
    var result = new StringBuilder("{");
    for (int i = 0; i < attrs.getLength(); i++)
    {
        if (i > 0) result.append(", ");
        result.append(jsonEscape(attrs.item(i).getNodeName()));
        result.append(": ");
        result.append(jsonEscape(attrs.item(i).getNodeValue()));
    }
    result.append("}");
    return result;
}
}
```
```

| API | Version |
|---|---|
| `javax.xml.parsers.DocumentBuilderFactory` | `1.4` |

- `static DocumentBuilderFactory newInstance()`  
  returns an instance of the `DocumentBuilderFactory` class.
- `DocumentBuilder newDocumentBuilder()`  
  returns an instance of the `DocumentBuilder` class.