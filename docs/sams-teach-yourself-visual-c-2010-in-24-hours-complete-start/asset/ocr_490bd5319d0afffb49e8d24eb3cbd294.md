# ## Understanding the XML DOM

For you to programmatically read and manipulate an XML document, it must be represented in memory through the XML Document Object Model (DOM). The DOM provides a common and structured way XML data is represented in memory and is most commonly used for reading XML data into memory to change its structure, add or remove elements, or modify the data contained in an element.

An example XML document is shown in Listing 14.1 and the corresponding DOM structure is shown in Figure 14.1.

# **LISTING 14.1** XML Data

```
```xml
<books>
   <book>
      <title>Sams Teach Yourself Visual C# 2010 in 24 Hours</title>
      <isbn-10>0-672-33101-2</isbn-10>
      <author>Dorman</author>
      <price currency="US">39.99</price>
      <publisher>
         <name>Sams Publishing</name>
         <state>IN</state>
      </publisher>
   </book>
</books>
```
```

**FIGURE 14.1** XML DOM representation

![](bbox=[0.2, 0.54, 0.85, 0.82])

In Figure 14.1, each circle represents an element in the XML data. The lighter circle represents the **document root**, or starting, element. The document root node is the top-level node containing the document itself. All nodes except the document root have a single parent node, which is the node directly above them. When nodes have