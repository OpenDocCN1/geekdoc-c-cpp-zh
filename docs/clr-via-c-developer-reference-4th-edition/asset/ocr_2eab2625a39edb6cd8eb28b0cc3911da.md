# TABLE 24-1 StreamingContext's Public Read-Only Properties

| Member Name | Member Type | Description |
|---|---|---|
| State | StreamingContextStates | A set of bit flags indicating the source or destination of the objects serialized/deserialized |
| Context | Object | A reference to object that contains any user-desired context information |

A method that receives a StreamingContext structure can examine the State property's bit flags to determine the source or destination of the objects serialized/deserialized. Table 24-2 shows the possible bit flag values.

# TABLE 24-2 StreamingContext's Flags

| Flag Name | Flag Value | Description |
|---|---|---|
| CrossProcess | 0x0001 | The source or destination is a different process on the same machine |
| CrossMachines | 0x0002 | The source or destination is on a different machine. |
| File | 0x0004 | The source or destination is a file. Don't assume that process will deserialize the data, and |
| Persistence | 0x0008 | The source or destination is a store as a database or file. Don't assume the same process will deserialize the data, and |
| Remoting | 0x0010 | The source or destination is remoting to an unknown location. The location may be on the same machine but also may be on another machine. |
| Other | 0x0020 | The source or destination is unknown. |
| Clone | 0x0040 | The object graph is cloned. The serialization code may assume the same process will deserialize the data, and it is safe to access handles or unmanaged resources. |
| CrossAppDomain | 0x0080 | The source or destination is a different AppDomain. |
| All | 0x00FF | The source or destination may be any of the above contexts. This is the default context. |

Now that you know how to get this information, let's discuss how you would set this information. The IFormatter interface (which is implemented by both the BinaryFormatter and the SoapFormatter types) defines a read/write StreamingContext property called Context. When you construct a formatter, it initializes its Context property so that StreamingContext-States is set to All and the reference to the additional state object is set to null.

After a formatter is constructed, you can construct a StreamingContext using any of the StreamingContext flags, and you can optionally pass a reference to an object containing any additional context information you need. Now, all you need to do is set the formatter's Context property with this new StreamingContext object before calling the formatter's Serialize or Deserialize methods. Code demonstrating how to tell a formatter that you are serializing/deserializing an object graph for the sole purpose of cloning all the objects in the graph is shown in the DeepClone method presented earlier in this chapter.