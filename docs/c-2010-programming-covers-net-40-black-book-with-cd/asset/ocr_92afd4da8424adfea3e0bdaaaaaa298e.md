a stream/document. Finally, you call the Serialize() method of the XmlSerializer class by passing two parameters. One of these parameters is a stream/writer object and the other is the object that you want to serialize.

In addition, you can also deserialize an object by using another part of your application or a separate application. After deserialization, an object returns to the state in which it was before serialization. For deserializing an object, you first create two objects—an XmlSerializer object and a stream/reader object. After that, you call the Deserialize() method of the XmlSerializer class by passing the stream/reader object as a parameter. The Deserialize() method returns the deserialized object that needs to be cast to the correct type.

The object, which you want to serialize, and the XML document are linked with the help of a custom C# attribute. A C# attribute is a type of declarative information that can be retrieved by the Common Language Runtime (CLR) at runtime. In addition, it describes how the object should be serialized. It can be created by using a tool, called xsd.exe, which is included in .NET Framework 4.0. The characteristics of xsd.exe are as follows:

+   - Generates an XML schema from an XML file
+   - Generates an XML schema from an External Data Representation (XDR) schema file
+   - Generates DataSet objects from an XSD schema file
+   - Generates an XSD file from classes you have already developed
+   - Generates schemas from the types defined in runtime assembly files
+   - Generates runtime classes that contain custom attributes for XmlSerialization

Now, let’s move on to the Immediate Solutions section, where we implement the concepts described in the In Depth section.