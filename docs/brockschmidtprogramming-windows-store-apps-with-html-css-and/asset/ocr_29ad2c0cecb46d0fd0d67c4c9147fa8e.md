to bind within nested object structures (`obj1.obj2.prop3`, etc.).

+   * `addProperty` Adds a new property to the object that is automatically enabled for binding (it adds the same properties and methods that `expandProperties` does).
+   * `removeProperty` Removes a property altogether from the object.

The `Binding.dynamicObservableMixin` object, I should note, is exactly the same as `mixin` except for one small difference. If you take an observable class built with `mixin` and then derive a new class from it (see `WinJS.Class.derive`), the new class will not automatically be observable. If you build the base class with `dynamicObservableMixin`, on the other hand, its observability will apply to derived classes.

# ## Programmatic Binding and WinJS.Binding.bind

Taking a step back from the details now, we can see that the eight `mixin` methods, along with the `get` and `set` implementations from `expandProperties`, fulfill the requirements of an observable data source. With such a source in hand you can do some interesting things programmatically. First, you can call the object's `bind` method directly to hook up any number of additional actions manually. A couple of scenarios come to mind where this would apply:

+   * You set up two-way binding between a local data source and the app's UI, and want to also sync changes to the source with a back-end service. A second handler attached through `bind` would be called whenever the source is modified through any other means.
+   * You need to create an intermediate source object that combines and consolidates property changes from other sources, simplifying binding to a final target UI element. Calling `bind` directly in such cases is necessary because `Binding.processAll` specifically works with UI elements declared in HTML rather than arbitrary JavaScript objects.

The `notify` method, for its part, is something you can call directly to trigger notifications. This is useful with additional bindings that don't necessarily depend on the values themselves, just the fact that they changed. The major use case here is to implement computed properties—ones that change in response to another property value changing.

The WinJS binding engine also has some intelligent handling of multiple changes to the same source property. After the initial binding, further change notifications are asynchronous and multiple pending changes to the same property are coalesced. So, if in our example we made several changes to the name property in quick succession:

```
```javascript
login.name = "Kenichiro";
login.name = "Josh";
login.name = "Chris";
```
```

only one notification for the last value would be sent and that would be the value that shows up in bound targets.