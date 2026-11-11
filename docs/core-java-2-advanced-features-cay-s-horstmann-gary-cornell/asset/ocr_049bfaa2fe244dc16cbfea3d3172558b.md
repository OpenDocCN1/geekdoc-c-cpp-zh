A better approach is to build up a DOM tree with the contents of the document
and then write out the tree contents. The following sections discuss the details.

# 3.7.1 Documents without Namespaces

To build a DOM tree, you start out with an empty document. You can get an
empty document by calling the `newDocument` method of the `DocumentBuilder` class:

```
Document doc = builder.newDocument();
```

Use the `createElement` method of the Document class to construct the elements of your
document:

```
Element rootElement = doc.createElement(rootName);
Element childElement = doc.createElement(childName);
```

Use the createTextNode method to construct text nodes:

```
Text textNode = doc.createTextNode(textContents);
```

Add the root element to the document, and add the child nodes to their parents:

```
doc.appendChild(rootElement);
rootElement.appendChild(childElement);
childElement.appendChild(textNode);
```

As you build up the DOM tree, you may also need to set element attributes.
Simply call the setAttribute method of the Element class:

```
rootElement.setAttribute(name, value);
```

# 3.7.2 Documents with Namespaces

If you use namespaces, the procedure for creating a document is slightly different.

First, set the builder factory to be namespace-aware, then create the builder:

```
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
factory.setNamespaceAware(true);
builder = factory.newDocumentBuilder();
```

Then use the `createElementNS` instead of `createElement` to create any nodes:

```
String namespace = "http://www.w3.org/2000/svg";
Element rootElement = doc.createElementNS(namespace, "svg");
```

If your node has a qualified name with a namespace prefix, then any necessary
xml-ns-prefixed attributes are created automatically. For example, if you need SVG
inside XHTML, you can construct an element like this:

```
Element svgElement = doc.createElement(namespace, "svg:svg");
```