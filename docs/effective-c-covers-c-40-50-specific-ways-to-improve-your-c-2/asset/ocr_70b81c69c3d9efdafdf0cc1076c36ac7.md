```
object result = null;
if (storage.ContainsKey(key))
{
    result = storage[key];
}
return result;
}
```

```
public override string ToString()
{
    StringWriter message = new StringWriter();
    foreach (var item in storage)
    message.WriteLine("{0}:{1}", item.Key,
    item.Value);
    return message.ToString();
}
```

GetMetaObject() returns a new DynamicDictionaryMetaObject whenever it is called. Here's where the first complexity enters the picture. GetMetaObject() is called every time any member of the DynamicDictionary is invoked. If you call the same member ten times, GetMetaObject() gets called ten times. Even if methods are statically defined in DynamicDictionary2, GetMetaObject() will be called and can intercept those methods to invoke possible dynamic behavior. Remember that dynamic objects are statically typed as dynamic, and therefore have no compile-time behavior defined. Every member access is dynamically dispatched.

The DynamicMetaObject is responsible for building an Expression Tree that executes whatever code is necessary to handle the dynamic invocation. Its constructor takes the expression and the dynamic object as parameters. After being constructed, one of the Bind methods will be called. Its responsibility is to construct a DynamicMetaObject that contains the expression to execute the dynamic invocation. Let's walk through the two Bind methods necessary to implement the DynamicDictionary: BindSetMember and BindGetMember.

BindSetMember constructs an expression tree that will call DynamicDictionary2.SetDictionaryEntry() to set a value in the dictionary. Here's its implementation: