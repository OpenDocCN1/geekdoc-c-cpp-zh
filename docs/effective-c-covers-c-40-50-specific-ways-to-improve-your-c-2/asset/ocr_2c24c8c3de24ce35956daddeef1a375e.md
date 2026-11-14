```
result = null;
return false;
}
```

```
public override bool TrySetMember(SetMemberBinder binder,
    object value)
{
    string key = binder.Name;
    if (storage.ContainsKey(Key))
        storage[key] = value;
    else
        storage.Add(key, value);
    return true;
}
```

```
public override string ToString()
{
    StringWriter message = new StringWriter();
    foreach (var item in storage)
        message.WriteLine("{0}:\\t{1}", item.Key,
            item.Value);
    return message.ToString();
}
```

The dynamic property bag contains a dictionary that stores the property names and their values. The work is done in TryGetMember and TrySetMember.

TryGetMember examines the requested name (binder.Name), and if that property has been stored in the Dictionary, TryGetMember will return its value. If the value has not been stored, the dynamic call fails.

TrySetMember accomplishes its work in a similar fashion. It examines the requested name (binder.Name) and either updates or creates an entry for that item in the internal Dictionary. Because you can create any property, the TrySetMember method always returns true, indicating that the dynamic call succeeded.

DynamicObject contains similar methods to handle dynamic invocation of indexers, methods, constructors, and unary and binary operators. You can override any of those members to create your own dynamic members.