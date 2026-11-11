The header can be followed by a *document type definition* (DTD), such as

```
```xml
<!DOCTYPE web-app PUBLIC
    "-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
    "http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
```
```

DTDs are an important mechanism to ensure the correctness of a document, but they are not required. We will discuss them later in this chapter.

Finally, the body of the XML document contains the *root element*, which can contain other elements. For example,

```
```xml
<?xml version="1.0"?>
<!DOCTYPE configuration . . . >
<configuration>
    <title>
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </title>
    . . .
</configuration>
```
```

An element can contain child elements, text, or both. In the preceding example, the font element has two child elements, name and size. The name element contains the text "Helvetica".

![](bbox=[0.107, 0.588, 0.147, 0.619])

> > **TIP:** It is best to structure your XML documents so that an element contains *either* child elements or text. In other words, you should avoid situations such as
> >
> > ```xml
> > <font>
> >     Helvetica
> >     <size>36</size>
> > </font>
> > ```
> >
> > This is called *mixed content* in the XML specification. As you will see later in this chapter, you can simplify parsing if you avoid mixed content.

XML elements can contain attributes, such as

```
```xml
<size unit="pt">36</size>
```
```

There is some disagreement among XML designers about when to use elements and when to use attributes. For example, it would seem easier to describe a font as

```
```xml
<font name="Helvetica" size="36"/>
```
```

than