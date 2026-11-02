
A couple of additional demonstrations of calling these binding methods directly can also be found in scenarios 1 and 2 of the `Programmatic binding sample`, which doesn't use any declarative syntax at all. Scenario 1, for example, creates an observable source with `Binding.as` and wires it up with `bind` method to a couple of change handlers for two-way binding. (It employs the `WinJS.Utilities.query` and `WinJS.Utilities.QueryCollection.listen` methods, which are described in Appendix B.) Be mindful when looking at lines like this (js/1_BasicBinding.js):

```js
this.bindSource.bind("x", this.onXChanged.bind(this));
```

that the first `bind` method on the source object comes from `WinJS.Binding.mixin`, whereas the `bind` method on the `onXChanged` function is the standard JavaScript method to manage the `this` variable.

Scenario 2 demonstrates a coding construct called a binding descriptor that works in conjunction with the static helper method `WinJS.Binding.bind`. Yes, be aware! `WinJS.Binding.bind` is yet another `bind` method that's separate from a source object's `bind` that's defined in the mixins and separate from a function's `bind` method. Fortunately, you must always call `WinJS.Binding.bind` with its full name, and I'll refer to it this way to avoid confusion.

**Preview note** The current documentation for `WinJS.Binding.bind` is wrong, as it's just a copy of the mixin's `bind` documentation. The true documentation can be found in the `base.js` file of WinJS if you search on the full name. I have filed a bug on this.

I referred to `WinJS.Binding.bind` just now as a helper function, because it's basically a way to make a bunch of `bind` calls for properties of a complex object. Consider the source object that's created in scenario 2 of the `Programmatic binding sample` (js/2_BindingDescriptors.js):

```js
this.objectPosition = WinJS.Binding.as({
    position: { x: 10, y: 10 },
    color: { r: 128, g: 128, b: 128 }
});
```

If we wanted to set up binding relationships to each of these properties, we'd have to make a bunch of calls to `this.objectPosition.bind` like this:

```js
this.objectPosition.bind(this.objectPosition.x, <action>)
```

Such code gets ugly to write in a hurry. A binding descriptor, then, succinctly expresses the property-action mappings in a structure that matches the source object. The generic syntax is: `{ property: { sub-property: function(value) { . . . } } }`. Here's a concrete example from scenario 2 (js/2_BindingDescriptors.js):

```js
{
    position: {
        x: onPositionChange,
        y: onPositionChange
    },
    color: {
        r: onColorChange,
        g: onColorChange,
        b: onColorChange
    }
}
```

where onPositionChange and onColorChange both refresh the output in response to data changes.55 Scenario 1 of the Declarative binding sample has another example (js/1_BasicBinding.js):

```js
{
    color: {
        red: setBackColor,
        green: setBackColor,
        blue: setBackColor,
    }
}
```

When calling WinJS.Binding.bind, then, just pass the source object as the first argument and the binding descriptor as the second. As shown in the Declarative binding sample:

```js
return WinJS.Binding.bind(source, {
    color: {
        red: setBackColor,
        green: setBackColor,
        blue: setBackColor,
    }
});
```

The return value of WinJS.Binding.bind is an object with a cancel method that will clear out all these binding relationships (basically iterating through the structure calling unbind). In the Declarative binding sample, it returns this object from the binding initializer where it appears, which is actually very important. So let's now turn to initializers.

### Binding Initializers

When Binding.processAll encounters a data-win-bind attribute on an element, its main job is to take each <target property> : <source property> [<initializer>] string and turn it into a real binding relationship. Assuming that the data source is observable, this basically means calling the source's bind method with the source property name and some handler that will update the target property accordingly.

The purpose of the initializer function in this process is to define exactly what happens in that handler—that is, what happens to the target property in response to a source property update. In essence, an initializer provides the body of the handler given to the source's bind. In a simple binding relationship, that code might simply copy the source value to the target or it might involve a converter function. It could also consolidate multiple source properties—you can really do anything you want here. The key thing to remember is that the initializer itself will be called once and only once for each binding relationship, but the code it provides, such as a converter function, will be called every time the source property changes.

Now if you don't specify a custom initializer within data-win-bind, WinJS will always use a default, namely `WinJS.Binding.defaultBind`.36 It simply sets up a binding relationship that copies the source property's value straight over to the target property, as you'd expect. In short, the following two binding declarations have identical behavior:

```
data-win-bind="innerText: name"
data-win-bind="innerText: name defaultBind"
```

WinJS.Binding provides a number of other built-in initializers that can come in handy, most of which we've already encountered:

- `oneTime` Performs a one-time copy of the source property to the target property without setting up any other binding relationship. This is necessary when the source is a WinRT object, as noted earlier in "Sidebar: Binding to WinRT Objects."
- `setAttribute` and `setAttributeOneTime` Similar to defaultBind and oneTime but injects a call to the target element's `setAttribute` method instead of just copying the source value to a target property. See "Sidebar: Additional Property Syntax and Binding to WinJS Controls" earlier for more details.
- `addClassOneTime` Like setAttributeOneTime except that it interprets the source property as a class name and thus calls the target element's `classList.add` method to apply that class. This is useful when working with templates, as described later in this chapter.

Beyond these, we enter into the realm of custom initializers. The most common and simplest case is when you need to inject a converter into the binding relationship. All this takes on your part is to pass your conversion function to `WinJS.Binding.converter`, which returns the appropriate initializer (that's also marked for declarative processing). We did this in Tests 2, 3 and 4 of the BindingTests example. For Tests 3 and 4, for example, the initializer `LoginData.typeColorInitializer` is created as follows:

```js
WinJS.Namespace.define("LoginData", {
    // ...
    typeColorInitializer: WinJS.Binding.converter(userTypeToColor)
});
```

which we use in the HTML like so:

```html
<span id="loginName3"
      data-win-bind="innerText: name; style.color: userType LoginData.typeColorInitializer">
</span>
```

58 As shown earlier in "Sidebar: Binding to WinRT Objects," you can override the default initializer by providing your own as the fifth argument to `processAll` (after `skipRoot` and `bindingCache`). Though this argument doesn't appear in the MSDN documentation, it is described within the WinJS source file and is safe to use.

Doing anything more requires that you implement the initializer function directly. This is necessary, for instance, if you need to apply a converter to a WinRT data source, where normally you’re required to use the `oneTime` initializer already. A custom initializer can then do both steps at once.

Scenario 1 of the [Declarative binding sample](https://example.com) gives us an example of an initializer function (js/1_BasicBinding.js):

```javascript
var toCssColor = WinJS.Binding.initializer(
    function toCssColor(source, sourceProperty, dest, destProperty) {
        function setBackColor() {
            dest.style.backgroundColor =
                rgb(source.color.red, source.color.green, source.color.blue);
        }

        return WinJS.Binding.bind(source, {
            color: { red: setBackColor, green: setBackColor, blue: setBackColor, }
        });
    }
);

// A little helper function to convert from separate rgb values to a css color
function rgb(r, g, b) { return "rgb(" + [r, g, b].join(",") + ")"; }

WinJS.Namespace.define("BasicBinding", {
    toCssColor: toCssColor
});
```

`WinJS.Binding.initializer` is just an alias for `WinJS.Utilities.markSupportedForProcessing`, as discussed in Chapter 4, “Web Content and Services.” It makes sure you can reference this initializer from `processAll` and doesn’t add anything else where binding is concerned.

The arguments passed to your initializer clearly tell you which properties of `source` and target (`dest`) are involved in this particular relationship. The `source` and `dest` arguments are the same as the `dataContext` and `rootElement` arguments given to `processAll`, respectively. The `sourceProperty` and `destProperty` arguments are both arrays that contain the “paths” to their respective properties, where each part of the identifier is an element in the array. That is, if you have an identifier like `style.color` in data-win-bind, the path array will be `[style, color]`.

**Tip** If you find it tricky to set a breakpoint inside an initializer, just insert the `debugger` statement at the top and you’ll always stop at that point.

With all this information in hand, you can then set up whatever binding relationships you want by calling the source’s `bind` method with whatever properties and handlers you require. To duplicate the behavior of `oneTime`, as with WinRT sources, you wouldn’t call `bind` but instead just assign the value of the source property to the destination property.
