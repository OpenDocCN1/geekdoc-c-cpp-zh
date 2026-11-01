Looking at the list box, you can check that in the data tables that were created all the columns have the correct names and data types.

Something else you might want to note is that, because the previous two examples did not transfer any data to or from a database, no SqlDataAdapter or SqlConnection was defined. This shows the real flexibility of both the System.Xml namespace and ADO.NET: you can look at the same data in multiple formats. If you need to do a transform and show the data in HTML format, or if you need to bind the data to a grid, you can take the same data and, with just a method call, have it in the required format.

# SERIALIZING OBJECTS IN XML

Serializing is the process of persisting an object to disk. Another part of your application, or even a separate application, can deserialize the object, and it will be in the same state it was in prior to serialization. The .NET Framework includes a couple of ways to do this.

This section looks at the System.Xml.Serialization namespace, which contains classes used to serialize objects into XML documents or streams. This means that an object's public properties and public fields are converted into XML elements, attributes, or both.

The most important class in the System.Xml.Serialization namespace is XmlSerializer. To serialize an object, you first need to instantiate an XmlSerializer object, specifying the type of the object to serialize. Then you need to instantiate a stream/writer object to write the file to a stream/document. The final step is to call the Serialize() method on the XmlSerializer, passing it the stream/writer object and the object to serialize.

Data that can be serialized can be primitive types, fields, arrays, and embedded XML in the form of XmlElement and XmlAttribute objects.

To deserialize an object from an XML document, you reverse the process in the previous example. You create a stream/reader and an XmlSerializer object and then pass the stream/reader to the Deserialize() method. This method returns the deserialized object, although it needs to be cast to the correct type.

> > The XML serializer cannot convert private data, only public data, and it cannot serialize object graphs. However, these should not be serious limitations; by carefully designing your classes, you should be able to easily avoid these issues. If you do need to be able to serialize public and private data as well as an object graph containing many nested objects, you will want to use the System.Runtime.Serialization.Formatters.Binary namespace.

Some of the other tasks that you can accomplish with System.Xml.Serialization classes are:

+   - Determine if the data should be an attribute or element
+   - Specify the namespace
+   - Change the attribute or element name

The links between your object and the XML document are the custom C# attributes that annotate your classes. These attributes are what are used to inform the serializer how to write out the data. The xsd.exe tool, which is included with the .NET Framework, can help create these attributes for you. xsd.exe can do the following:

+   - Generate an XML schema from an XDR schema file
+   - Generate an XML schema from an XML file