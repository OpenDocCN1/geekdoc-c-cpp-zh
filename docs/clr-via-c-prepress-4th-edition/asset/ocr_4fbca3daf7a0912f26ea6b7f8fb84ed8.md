This method returns an array of Objects where each element identifies the value of a field in the object being serialized. This Object array and the MemberInfo array are parallel. That is, element 0 in the Object array is the value of the member identified by element 0 in the MemberInfo array.

+   3. The formatter writes the assembly’s identity and the type’s full name to the stream.

+   4. The formatter then enumerates over the elements in the two arrays, writing each member’s name and value to the stream.

The following steps describe how a formatter automatically deserializes an object whose type has the SerializableAttribute attribute applied to it:

+   5. The formatter reads the assembly’s identity and full type name from the stream. If the assembly is not currently loaded into the AppDomain, it is loaded (as described earlier). If the assembly can’t be loaded, a SerializationException exception is thrown and the object cannot be deserialized. If the assembly is loaded, the formatter passes the assembly identity information and the type’s full name to FormatterServices’ static GetTypeFromAssembly method:

```
```csharp
public static Type GetTypeFromAssembly(Assembly assem, String name);
```
```

This method returns a System.Type object indicating the type of object that is being deserialized.

+   6. The formatter calls FormatterServices’s static GetUninitializedObject method:

```
```csharp
public static Object GetUninitializedObject(Type type);
```
```

This method allocates memory for a new object but does not call a constructor for the object. However, all the object’s bytes are initialized to null or 0.

+   7. The formatter now constructs and initializes a MemberInfo array as it did before by calling the FormatterServices’s GetSerializableMembers method. This method returns the set of fields that were serialized and that need to be deserialized.

+   8. The formatter creates and initializes an Object array from the data contained in the stream.

+   9. The reference to the newly allocated object, the MemberInfo array, and the parallel Object array of field values is passed to FormatterServices’ static PopulateObjectMembers method:

```
```csharp
public static Object PopulateObjectMembers(
    object obj, MemberInfo[] members, Object[] data);
```
```

This method enumerates over the arrays, initializing each field to its corresponding value. At this point, the object has been completely deserialized.