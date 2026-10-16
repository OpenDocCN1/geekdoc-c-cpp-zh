used to serialize objects into XML documents or streams. This means that an object’s public properties and public fields are converted into XML elements, attributes, or both.

The most important class in the System.Xml.Serialization namespace is XmlSerializer. To serialize an object, you first need to instantiate an XmlSerializer object, specifying the type of the object to serialize. Then you need to instantiate a stream/writer object to write the file to a stream/document. The final step is to call the Serialize method on the XMLSerializer, passing it the stream/writer object and the object to serialize.

Data that can be serialized can be primitive types, fields, arrays, and embedded XML in the form of XmlElement and XmlAttribute objects. To deserialize an object from an XML document, you reverse the process in the previous example. You create a stream/reader and an XmlSerializer object and then pass the stream/reader to the Deserialize method. This method returns the deserialized object, although it needs to be cast to the correct type.

> NOTE The XML serializer cannot convert private data—only public data—and it cannot serialize cyclic object graphs. However, these are not serious limitations; by carefully designing your classes, you should be able to easily avoid these issues. If you do need to be able to serialize public and private data as well as an object graph containing many nested objects, you can use the runtime or the data contract serialization mechanisms.

The sample code makes use of the following dependencies and namespaces:

# Dependencies

```
NETStandard.Library
```

```
System.Xml.XmlDocument
```

```
System.Xml.XmlSerializer
```

# Namespaces

```
System.IO
```

```
System.Xml
```

```
System.Xml.Serialization
```

```
static System.Console
```

# Serializing a Simple Object

Let’s start serializing a simple object. The class Product has XML attributes from the namespace System .Xml.Serialization applied to specify whether a property should be serialized as XML element or attribute. The XmlElement attribute specifies the property to serialize as