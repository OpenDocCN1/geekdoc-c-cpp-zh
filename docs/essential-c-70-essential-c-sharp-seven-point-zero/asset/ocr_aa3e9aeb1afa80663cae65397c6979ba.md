Listing 18.25 serializes and deserializes a Document object. Serialization involves instantiating a formatter (System.Runtime.Serialization.Formatters.Binary.BinaryFormatter, in this example) and calling Serialization() with the appropriate stream object. Deserializing the object simply involves calling the formatter's Deserialize() method, specifying the stream that contains the serialized object as an argument. However, given that the return from Deserialize() is of type object, you also need to cast it specifically to the type that was serialized.

Notice that serialization occurs for the entire object graph (all items associated with the serialized object [Document] via a field). Therefore, all fields in the object graph also must be serializable.

# **System.NonSerializable**

Fields that are not serializable should be decorated with the System.NonSerializable attribute, which tells the serialization framework to ignore them. The same attribute should appear on fields that should not be persisted for use-case reasons. Passwords and Windows handles are good examples of fields that should not be serialized: Windows handles because they change each time a window is re-created, and passwords because data serialized into a stream is not encrypted and can be readily accessed. Consider the Notepad view of the serialized document in Figure 18.2.

![](bbox=[0.28, 0.65, 0.72, 0.75])

**FIGURE 18.2: BinaryFormatter Does Not Encrypt Data**

Listing 18.25 set the Title field, and the resultant *.BIN file includes the text in plain view.