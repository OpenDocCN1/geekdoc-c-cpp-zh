(or inner exception) will save the original SqlException in the Inner-Exception property. That way, when requiring additional details about the original exception, developers can retrieve the exception from the InnerException property (for example, exception.InnerException).

# ADVANCED TOPIC

# Serializable Exceptions

Serializable objects are objects that the runtime can persist into a stream—a file stream, for example—and then reinstantiate out of the stream. In the case of exceptions, this may be necessary for certain distributed communication technologies. To support serialization, exception declarations should include the System.SerializableAttribute attribute or they should implement ISerializable. Furthermore, they must include a constructor that takes System.Runtime.Serialization.SerializationInfo and System.Runtime.Serialization.StreamingContext. Listing 10.5 shows an example of using System.SerializableAttribute.

```
LISTING 10.5: Defining a Serializable Exception

// Supporting serialization via an attribute
[Serializable]
class DatabaseException : System.ApplicationException
{
    // ...

    // Used for deserialization of exceptions
    public DatabaseException(
        SerializationInfo serializationInfo,
        StreamingContext context)
    {
        //...
    }
}
```

The preceding DatabaseException example demonstrates both the attribute and the constructor requirement for making an exception serializable.