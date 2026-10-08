# Building Online Code Snippet Providers

With code snippets, you can create an online repository where you can select snippets categorized by your interest, and then download them to your machine. While snippets can be converted into the .snippet file format, you can import them with Code Snippets Manager or create your own custom template.

When you have a code snippet, you can upload it to a site with its .snippet file format. The structure of a snippet file contains a few elements (such as the <Keywords> and <HelpUrl> child elements of <Header>) is intended to be used by online snippet providers to help with the categorization and organization of snippets.

You can even add new information to your code snippets, although the current code snippet scheme does not allow creating your own elements or attributes. Despite this schema constraint, you can add your own elements and attributes, as shown in the following example:

```
<Snippet>
<Code Language="C#" MyAttr="myfile">
<![CDATA[Console.WriteLine();]]>
</Code>
<XmlElement Element="#####">\XmlElement>
</Snippet>
```

Here, MyElement and MyAttr are invalid elements by schema definition, but in reality, the Code Snippets Manager does not validate the .snippet file against the schema. While the Code Snippets Manager finds the elements it looks for, it remains happy, and simply does not take care of other elements and attributes.

> Although you can do this trick, it is not recommended. You cannot be sure that a future release of Visual Studio will not change this undocumented behavior. If you want to provide some kind of extension, you can use the kind attribute of the  element or the <Function> element nested inside <Object>.

# SNIPPET EDITORS

Editing .snippet files in Visual Studio is easy when you attach the appropriate XSD schema file to it, because IntelliSense helps by listing elements, attributes, and values in the current context. However, the user experience through editing the XML file (even with IntelliSense) is not always pleasant. The less complex code of your XML file is the  element encapsulating the body of the code. The more complex code template you create, the larger the <Declaration> part is. As you use the declarations longer than one or two pages on the screen, you can easily lose the focus. You must manage up and understand what the code template is about.

The community recognized that the built-in Visual Studio editing support can be improved with other tools that provide code template editing similar to editing the original code. Tag 3-5 shows a few snippet editors created and supported by the community.