| Member Name | Member Type | Description |
|---|---|---|
| **MemberType** | **MemberTypes** (enum) property | Returns the kind of member (field, constructor, method, property, event, type (non-nested type or nested type). |
| **DeclaringType** | **Type** property | Returns the **Type** that declares the member. |
| **ReflectedType** | **Type** property | Returns the **Type** used to obtain this member. |
| **Module** | **Module** property | Returns the **Module** that declares the member. |
| **MetadataToken** | **Int32** property | Returns the metadata token (within the module) that identifies the member. |
| **GetCustomAttributes** | Method returning **Object[]** | Returns an array in which each element identifies an instance of a custom attribute applied to this member. Custom attributes can be applied to any member. Use this method with assemblies that have not been loaded in the “reflection only” context. |
| **GetCustomAttributesData** | Method returning **IList<CustomAttributeData>** | Returns a collection in which each element identifies an instance of a custom attribute applied to this member. Custom attributes can be applied to any member. Even though **Assembly** does not derive from **MemberInfo**, it provides the same method that can be used with assemblies. |
| **IsDefined** | Method returning **Boolean** | Returns **true** if at least one instance of the specified custom attribute is applied to the member. |

Most of the properties mentioned in Table 23-1 are self-explanatory. However, developers frequently confuse the `DeclaringType` and `ReflectedType` properties. To fully understand these properties, let’s define the following type:

```
```csharp
public sealed class MyType {
    public override String ToString() { return null; }
}
```
```

What would happen if the following line of code executed?

```
```csharp
MemberInfo[] members = typeof(MyType).GetMembers();
```
```