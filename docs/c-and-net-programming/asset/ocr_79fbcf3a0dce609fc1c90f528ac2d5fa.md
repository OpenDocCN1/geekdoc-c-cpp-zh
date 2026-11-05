```
```xml
<title>C# Programming</title>

<author>Ravi Wani</author>

<chapters>

  <chapter name="Introduction to XML"/>

</chapters>

</book>

</journal>
```
```

First line is the element journal.
Use the WriteStartElement method to write this to the writer:

```
```csharp
writer.WriteStartElement("journal");
```
```

Don’t close this element until all Book elements are written. Thus, the next node to add is an opening Book element in the writer.

```
```csharp
writer.WriteStartElement("book");
```
```

The title element (<title>C# Programming</title>) is to be written.

This type differs from earlier because it has a specific value. As there are no more attributes on the title element, use the WriteElementString method:

```
```csharp
writer.WriteElementString("title", "C# Programming");
```
```

```
```csharp
writer.WriteElementString("author", "Ravi Wani");
writer.WriteStartElement("chapters");
```
```

Now, element, chapters, are with an attribute, name.

Here, **first write the start** of the element, then write the attributes, and finally, close element.

```
```csharp
writer.WriteStartElement("chapter");

writer.WriteAttributeString("name", "Control Structures");

writer.WriteEndElement();
```
```

There is no need to say which element is to be closed, because the writer will automatically write the closing tag for the **last-opened element**, which, in this case, is chapter.

Now close the remaining elements in the same fashion,

```
```csharp
writer.WriteEndElement();

writer.WriteEndElement();
```
```