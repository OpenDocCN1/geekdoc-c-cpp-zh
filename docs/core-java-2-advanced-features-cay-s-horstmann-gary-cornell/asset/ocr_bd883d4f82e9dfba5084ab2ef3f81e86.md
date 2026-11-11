If you expect only subelements, you can ignore the whitespace:

```
```java
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    if (child instanceof Element)
    {
        Element childElement = (Element) child;
        . . .
    }
}
```
```

Now you look at only two elements, with tag names name and size.

As you will see in the next section, you can do even better if your document has a DTD. Then the parser knows which elements don’t have text nodes as children, and it can suppress the whitespace for you.

When analyzing the name and size elements, you want to retrieve the text strings that they contain. Those text strings are themselves contained in child nodes of type Text. You know that these Text nodes are the only children, so you can use the getFirstChild method without having to traverse another NodeList. Then, use the getData method to retrieve the string stored in the Text node.

```
```java
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    if (child instanceof Element)
    {
        Element childElement = (Element) child;
        Text textNode = (Text) childElement.getFirstChild();
        String text = textNode.getData().trim();
        if (childElement.getTagName().equals("name"))
            name = text;
        else if (childElement.getTagName().equals("size"))
            size = Integer.parseInt(text);
    }
}
```
```

> > **TIP:** It is a good idea to call `trim` on the return value of the `getData` method. If the author of an XML file puts the beginning and the ending tags on separate lines, such as:
> >
> > ```xml
> > <size>
> >     36
> > </size>
> > ```
> >
> > then the parser will include all line breaks and spaces in the text node data. Calling the `trim` method removes the whitespace surrounding the actual data.