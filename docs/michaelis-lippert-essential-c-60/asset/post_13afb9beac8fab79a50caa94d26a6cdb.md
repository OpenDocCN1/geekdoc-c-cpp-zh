
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

## Versioning the Serialization

One more serialization point deserves mention: versioning. Objects such as documents may be serialized using one version of an assembly and deserialized using a newer version; the reverse may also occur. If the programmer is not paying sufficient attention, however, version incompatibilities can easily be introduced in this process, sometimes unexpectedly. Consider the scenario shown in Table 17.1.

## TABLE 17.1: Deserialization of a New Version Throws an Exception

| Step | Description | Code |
|---|---|---|
| 1. | Define a class decorated with System.SerializableAttribute. | `[Serializable]`<br>`class Document` |
| 2. | Add a field or two (public or private) of any serializable type. | `{`<br>`    public string Title;`<br>`    public string Data;`<br>`}` |
| 3. | Serialize the object to a file called *.v1.bin. | `Stream stream;`<br>`Document documentBefore = new Document();`<br>`documentBefore.Title = "A cacophony of ramblings from my potpourri of notes";`<br>`Document documentAfter;`<br>`using (stream = File.Open(documentBefore.Title + ".bin", FileMode.Create))`<br>`{`<br>`    BinaryFormatter formatter = new BinaryFormatter();`<br>`    formatter.Serialize(stream, documentBefore);`<br>`}` |
| 4. | Add an additional field to the serializable class. | `[Serializable]`<br>`class Document`<br>`{`<br>`    public string Title;`<br>`    public string Author;`<br>`    public string Data;`<br>`}` |
| 5. | Deserialize the *v1.bin file into the new object (Document) version. | `using (stream = File.Open(documentBefore.Title + ".bin", FileMode.Open))`<br>`{`<br>`    BinaryFormatter formatter = new BinaryFormatter();`<br>`    documentAfter = (Document)formatter.Deserialize(stream);`<br>`}` |

In Listing 17.29, CustomAttribute is the full name of the decorating attribute.

SerializableAttribute translates to a set bit within the metadata tables. This makes SerializableAttribute a pseudoattribute—that is, an attribute that sets bits or fields in the metadata tables.

## Programming with Dynamic Objects

The introduction of dynamic objects in C# 4.0 simplified a host of programming scenarios and enabled several new ones previously not available. At its core, programming with dynamic objects enables developers to code operations using a dynamic dispatch mechanism that the runtime will resolve at execution time, rather than the compiler verifying and binding to it at compile time.

Why? Many times, objects are inherently not statically typed. Examples include loading data from an XML/CSV file, a database table, the Internet Explorer DOM, or COM’s IDispatch interface, or calling code in a dynamic language such as an IronPython object. C# 4.0’s Dynamic object support provides a common solution for talking to runtime environments that don’t necessarily have a compile-time–defined structure. In the initial implementation of dynamic objects in C# 4.0, four binding methods are available:

- 1. Using reflection against an underlying CLR type
- 2. Invoking a custom IDynamicMetaObjectProvider that makes available a DynamicMetaObject
- 3. Calling through the IUnknown and IDispatch interfaces of COM
- 4. Calling a type defined by dynamic languages such as IronPython

Of these four approaches, we will delve into the first two. The principles underlying them translate seamlessly to the remaining cases—COM interoperability and dynamic language interoperability.

## Invoking Reflection Using dynamic

One of the key features of reflection is the ability to dynamically find and invoke a member on a particular type based on an execution-time identification of the member name or some other quality, such as an attribute (see Listing 17.3). However, C# 4.0’s addition of dynamic objects provides

a simpler way of invoking a member by reflection, assuming compile-time knowledge of the member signature. To reiterate, this restriction states that at compile time we need to know the member name along with the signature (the number of parameters and whether the specified parameters will be type-compatible with the signature). Listing 17.30 (with Output 17.10) provides an example.

## LISTING 17.30: Dynamic Programming Using “Reflection”

```
using System;

// ...
dynamic data = "Hello! My name is Inigo Montoya";
Console.WriteLine(data);
data = (double)data.Length;
data = data * 3.5 + 28.6;
if(data == 2.4 + 112 + 26.2)
{
    Console.WriteLine(
        $"{ data } makes for a long triathlon.");
}
else
{
    data.NonExistentMethodCallStillCompiles();
}
// ...
```

## OUTPUT 17.10

```
Hello!  My name is Inigo Montoya
140.6 makes for a long triathlon.
```

In this example, there is no explicit code for determining the object type, finding a particular MemberInfo instance, and then invoking it. Instead, data is declared as type dynamic and methods are called against it directly. At compile time, there is no check as to whether the members specified are available, or even a check regarding which type underlies the dynamic object. Hence, it is possible at compile time to make any call so long as the syntax is valid. At compile time, it is irrelevant whether there is really a corresponding member.

However, type safety is not abandoned altogether. For standard CLR types (such as those used in Listing 17.30), the same type checker

normally used at compile time for non-dynamic types is instead invoked at execution time for the dynamic type. Therefore, at execution time, if no such member is available, the call will result in a Microsoft.CSharp.RuntimeBinder.RuntimeBinderException.

Note that this capability is not nearly as flexible as the reflection described earlier in the chapter, although the API is undoubtedly simpler. The key difference when using a dynamic object is that it is necessary to identify the signature at compile time, rather than determine things such as the member name at runtime (as we did when parsing the command-line arguments).

## dynamic Principles and Behaviors

Listing 17.30 and the accompanying text reveal several characteristics of the dynamic data type.

- dynamic is a directive to the compiler to generate code.
- dynamic involves an interception mechanism so that when a dynamic call is encountered by the runtime, it can compile the request to CIL and then invoke the newly compiled call. (See the Advanced Topic titled “dynamic Uncovered” later in this chapter for more details.)
- The principle at work when a type is assigned to dynamic is to conceptually “wrap” the original type so that no compile-time validation occurs. Additionally, when a member is invoked at runtime, the “wrapper” intercepts the call and dispatches it appropriately (or rejects it). Calling GetType() on the dynamic object reveals the type underlying the dynamic instance—it does not return dynamic as a type.

- Any type that converts to object will convert to dynamic.
- In Listing 17.29, we successfully cast both a value type (double) and a reference type (string) to dynamic. In fact, all types can successfully be converted into a dynamic object. There is an implicit conversion from any reference type to dynamic. Similarly, there is an implicit conversion (a boxing conversion) from a value type to dynamic. In addition, there is an implicit conversion from dynamic to dynamic. This is perhaps obvious, but with dynamic this process is more complicated than simply copying the “pointer” (address) from one location to the next.
