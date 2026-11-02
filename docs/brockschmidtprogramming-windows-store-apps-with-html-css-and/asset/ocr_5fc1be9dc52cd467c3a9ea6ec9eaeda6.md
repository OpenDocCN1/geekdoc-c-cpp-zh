```
```javascript
toCssColor: toCssColor
});
```
```

Clearly, there's more going on here than just creating a simple converter as we did before, including use of the methods `WinJS.Binding.initialize` and `WinJS.Binding.bind`. Now is a good time, then, to peek under the covers to see how initializers work and what functions like `bind` are doing.

# ## Under the Covers: Binding mixins

Earlier in the "One-Way Binding" section I spelled out three requirements for an observable object: it maintains a list of bindings, provides methods to manage that list, and iterates through that list to update any target properties when source properties change. And we saw that `Binding.as` and `Binding.define` let you easily add such structures to a source object or class definition (you can find the source for both in the WinJS base.js file).

Both `as` and `define` create an observable object from an existing one by adding the necessary methods that the rest of `WinJS.Binding` requires. (This is done through mixins; to review details on `WinJS.Class.mix` and mixins, refer to Appendix B, "WinJS Extras.")

The `as` method, for its part, assumes that the data source is just a plain object (and not a `Date`, `Array`, or `nonobject`) and creates a proxy object around it using an internal `WinJS` class called `ObservableProxy`. You wouldn't instantiate this class directly, of course, but it's instructive to look at its definition, where `data` is the object you give to `as`:

```
```javascript
var ObservableProxy = WinJS.Class.mix(function (data) {
    this._initObservable(data);
    Object.defineProperties(this, expandProperties(data));
}, dynamicObservableMixin);
```
```

The call to `_initObservable` on the data source turns out to be very important. All it does is ensure that the class has a property called `_backingData` that's set to the original source. Without this you'd see a bunch of exceptions at run time.

`Binding.define` does pretty much the same thing except that its purpose is to create a constructor for an observable object class, rather than just wrapping an existing instance. It's how you define your own variant of the internal `ObservableProxy` class we see above.

You can also create an observable source manually, as shown in Scenario 3 of the Programmatic binding sample. Here it defines a `RectangleSprite` class with `Class.define` and then makes it observable (and adds a few more observable properties) as follows (`is/3.CreatingBindableTypes.js`):

```
```javascript
WinJS.Class.mix(RectangleSprite,
    WinJS.Binding.mixin,
    WinJS.Binding.expandProperties({ position: 0, r: 0, g: 0, b: 0 })
);
```
```

Note that the `RectangleSprite` constructor in this case must call `this._initObservable()` or else none of the binding will work (that is, the app will crash and burn). This is the only case I know of where