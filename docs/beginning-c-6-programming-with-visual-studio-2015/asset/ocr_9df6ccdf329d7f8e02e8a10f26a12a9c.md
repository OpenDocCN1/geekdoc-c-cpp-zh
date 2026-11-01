Recall that the is operator enables you to examine the type of an object, and it returns true if the instance is of the specified type. Even though the root node is declared as an XmlNode, that is merely the base type of the objects you are going to work with. By using the is operator to test the type of the objects, you are able to determine the type of the object at runtime and select the action to perform based on that.

Inside the FormatText method you generate the text for the textbox. You have to know the type of the current instance of root because the information you want to display is obtained differently for different elements: You want to display the name of XmlElements and the value of XmlText elements.

# Changing the Values of Nodes

Before you examine how to change the value of a node, it is important to realize that very rarely is the value of a node a simple thing. In fact, you will find that although all of the classes that derive from XmlNode include a property called Value, it very rarely returns anything useful to you. Although this can feel like a bit of a letdown at first, you'll find it is actually quite logical. Examine the books example from earlier:

```
<books>
  <book>
    <title>Beginning Visual C# 2015</title>
    <author>Benjamin Perkins et al</author>
    <code>096689</code>
  </book>
  <book>
</books>
```

Every single tag pair in the document resolves into a node in the DOM. Remember that when you looped through all the nodes in the document, you encountered a number of XmlElement nodes and three XmlText nodes. The XmlElement nodes in this XML are <books>, <book>, <title>, <author>, and <code>. The XmlText nodes are the text between the starting and closing tags of title, author, and code. Although it could be argued that the value of title, author, and code is the text between the tags, that text is itself a node; and it is that node that actually holds the value. The other tags clearly have no value associated with them other than other nodes.

The following line is in the if block near the top of the code in the earlier FormatText method. It executes when the current node is an XmlText node.

```
text += node.Value;
```

You can see that the Value property of the XmlText node instance is used to get the value of the node.

Nodes of the type XmlElement return null if you use their Value property, but it is possible to get the information between the starting and closing tags of an XmlElement if you use one of two other methods: InnerText and InnerXml. That means you are able to manipulate the value of nodes using two methods and a property, as described in Table 19-3.