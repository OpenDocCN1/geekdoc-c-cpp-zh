# # REGISTERING CALLBACKS

Now that we've seen what each kind of callback can do, let's explore how each kind of callback is registered, because the registration method has implications for how each of the callbacks should be implemented and how it can be used.

The PropertyChangedCallback and CoerceValueCallback are passed as part of the PropertyMetadata constructor:

```
new PropertyMetadata(<defaultValue>,
<PropertyChangedCallback>,
<CoerceValueCallback>)
```

Because the constructor parameters are delegates, you'll need to create instances of the appropriate delegate type. You'll usually do that inside the constructor, because there's no need to have the delegate types hanging around:

```
new PropertyMetadata(<defaultValue>,
new PropertyChangedCallback(<method>),
new CoerceValueCallback(<method>))
```

If you want to pass a CoerceValueCallback but not a PropertyChangedCallback, you can pass null to the PropertyMetadata constructor:

```
new PropertyMetadata(<defaultValue>,
null,
new CoerceValueCallback(<method>))
```