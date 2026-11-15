Exception. This is because the formatter looks for data corresponding to the new field within the stream. Failure to locate such data throws an exception.

To avoid this, the 2.0 framework and later includes a System.Runtime.Serialization.OptionalFieldAttribute. When you require backward compatibility, you must decorate serialized fields—even private ones—with OptionalFieldAttribute (unless, of course, a latter version begins to require it).

Unfortunately, System.Runtime.Serialization.OptionalFieldAttribute is not supported in the earlier framework version. Instead, it is necessary to implement ISerializable, just as you did for encryption, saving and retrieving only the fields that are available. Assuming the addition of the Author field, for example, the implementation shown in Listing 17.26 is required for backward-compatibility support prior to the 2.0 framework.

# LISTING 17.26: Backward Compatibility Prior to the 2.0 Framework

```
[Serializable]
public class VersionableDocument : ISerializable
{
    enum Field
    {
        Title,
        Author,
        Data,
    }

    public VersionableDocument()
    {
    }

    public string Title;
    public string Author;
    public string Data;

    #region ISerializable Members
    public void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue(Field.Title.ToString(), Title);
        info.AddValue(Field.Author.ToString(), Author);
        info.AddValue(Field.Data.ToString(), Data);
    }
    public VersionableDocument(
```