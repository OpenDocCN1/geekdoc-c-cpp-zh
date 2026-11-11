# Listing 3.1 (Continued)

```
```java
else if (node instanceof CharacterData)
{
    return characterString((CharacterData) node, level);
}
else
{
    return pad(new StringBuilder(), level).append(
        jsonEscape(node.getClass().getName()));
}

private static Map<Character, String> replacements = Map.of('\b', "\\b", '\f',
    "\\f", '\n', "\\n", '\r', "\\r", '\t', "\\t", '"', "\\\"", '\\', "\\\\");

private static StringBuilder jsonEscape(String str)
{
    var result = new StringBuilder("\"");
    for (int i = 0; i < str.length(); i++)
    {
        char ch = str.charAt(i);
        String replacement = replacements.get(ch);
        if (replacement == null) result.append(ch);
        else result.append(replacement);
    }
    result.append("\"");
    return result;
}

private static StringBuilder characterString(CharacterData node, int level)
{
    var result = new StringBuilder();
    StringBuilder data = jsonEscape(node.getData());
    if (node instanceof Comment) data.insert(1, " Comment: ");
    pad(result, level).append(data);
    return result;
}

private static StringBuilder elementObject(Element elem, int level)
{
    var result = new StringBuilder();
    pad(result, level).append("{\n");
    pad(result, level + 1).append("\"name\": ");
    result.append(jsonEscape(elem.getTagName()));
    NamedNodeMap attrs = elem.getAttributes();
}
```
```