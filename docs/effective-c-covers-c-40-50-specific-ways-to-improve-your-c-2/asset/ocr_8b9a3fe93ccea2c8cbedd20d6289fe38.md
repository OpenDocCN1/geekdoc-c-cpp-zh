makes it a relatively simple exercise to create a dynamic class, if you can derive from DynamicObject.

For example, consider a class that implemented a dynamic property bag. When you first create the DynamicPropertyBag, it doesn't have any items, and therefore it doesn't have any properties. When you try to retrieve any property, it will throw an exception. You can add any property to the bag by calling the setter on that property. After adding the property, you can call the getter and access any of the properties.

```
```csharp
dynamic dynamicProperties = new DynamicPropertyBag();
```
```

```
```csharp
try
{
    Console.WriteLine(dynamicProperties.Marker);
}
catch (Microsoft.CSharp.RuntimeBinder.RuntimeBinderException)
{
    Console.WriteLine("There are no properties");
}
```
```

```
```csharp
dynamicProperties.Date = DateTime.Now;
dynamicProperties.Name = "Bill Wagner";
dynamicProperties.Title = "Effective C#";
dynamicProperties.Content = "Building a dynamic dictionary";
```
```

The implementation of the dynamic property bag requires overriding the TrySetMember and TryGetMember methods in the DynamicObject base class.

```
```csharp
class DynamicPropertyBag : DynamicObject
{
    private Dictionary<string, object> storage =
        new Dictionary<string, object>();

    public override bool TryGetMember(GetMemberBinder binder,
        out object result)
    {
        if (storage.ContainsKey(binder.Name))
        {
            result = storage[binder.Name];
            return true;
        }
    }
```
```