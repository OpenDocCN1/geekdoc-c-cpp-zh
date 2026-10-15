```
}
public string Title;
public string Data;

public static string Encrypt(string data)
{
    string encryptedData = data;
    // Key-based encryption ...
    return encryptedData;
}

public static string Decrypt(string encryptedData)
{
    string data = encryptedData;
    // Key-based decryption...
    return data;
}

#region ISerializable Members
public void GetObjectData(
    SerializationInfo info, StreamingContext context)
{
    info.AddValue(
        Field.Title.ToString(), Title);
    info.AddValue(
        Field.Data.ToString(), Encrypt(Data));
}

public EncryptableDocument(
    SerializationInfo info, StreamingContext context)
{
    Title = info.GetString(
        Field.Title.ToString());
    Data = Decrypt(info.GetString(
        Field.Data.ToString()));
}
#endregion
}
```

Essentially, the System.Runtime.Serialization.SerializationInfo object is a collection of name/value pairs. When serializing, the GetObject() implementation calls AddValue(). To reverse the process, you call one of the Get*() members. In this case, you encrypt and decrypt prior to serialization and deserialization, respectively.

# Versioning the Serialization

One more serialization point deserves mention: versioning. Objects such as documents may be serialized using one version of an assembly and deserialized using a newer version; the reverse may also occur. If the