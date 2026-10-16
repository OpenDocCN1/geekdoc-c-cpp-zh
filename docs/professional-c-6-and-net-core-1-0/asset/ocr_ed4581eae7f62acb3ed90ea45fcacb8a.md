```
```csharp
public override bool TryGetMember(GetMemberBinder binder, out object result)
{
	bool success = false;
	result = null;
	if (_dynamicData.ContainsKey(binder.Name))
	{
		result = _dynamicData[binder.Name];
		success = true;
	}
	else
	{
		result ="Property Not Found!";
		success = false;
	}
	return success;
}

public override bool TrySetMember(SetMemberBinder binder, object value)
{
	_dynamicData[binder.Name] = value;
	return true;
}

public override bool TryInvokeMember(InvokeMemberBinder binder,
	object[] args, out object result)
{
	dynamic method = _dynamicData[binder.Name];
	result = method((DateTime)args[0]);
	return result != null;
}
```
```

# In this example, you’re overriding three methods: TrySetMember, TryGetMember, and TryInvokeMember.

TrySetMember adds the new method, property, or field to the object. In this case, you store the member information in a Dictionary object. The SetMemberBinder object that is passed into the TrySetMember method contains the Name property, which is used to identify the element in the Dictionary.

The TryGetMember retrieves the object stored in the Dictionary based on the GetMemberBinder Name property.

Here is the code that makes use of the new dynamic object just created (code file DynamicSamples/DynamicSample/Program.cs):

```
```csharp
dynamic wroxDyn = new WroxDynamicObject();
wroxDyn.FirstName = "Bugs";
wroxDyn.LastName = "Bunny";
WriteLine(wroxDyn.GetType());
WriteLine($" {wroxDyn.FirstName} {wroxDyn.LastName} ");
```
```

It looks simple enough, but where is the call to the methods you override? That’s where the .NET Framework helps. DynamicObject handles the binding for you; all you have to do is reference the