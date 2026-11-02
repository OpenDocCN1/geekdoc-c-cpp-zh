
This gives the following result, in which I shamelessly publish a picture of my kid as a baby:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_283_0.png)

With WinJS we can accomplish the same thing by using a declarative syntax and a processing function. In markup, we use the attribute data-win-bind to map target properties of the containing element to properties of the source object. The processing function, WinJS.Binding.processAll, then creates the necessary code to implement those binding relationships. This follows the same idea as using the declarative data-win-control and data-win-options attributes instruct WinJS.UI.processAll how to instantiate controls, as we saw in Chapter 5.

The value of data-win-bind is a string of property pairs. Each pair's syntax is <target property> : <source property> [<initializer>] where the <initializer> is an optional function that determines how the binding relationship is set up.

Each property identifier can use dot notation as needed (see the sidebar coming up for additional syntax), and uses JavaScript property names. Property pairs are separated by a semicolon, as shown in the HTML for Test 2 in the example:

```
<section id="loginDisplay2">
<p>You are logged in as
<span id="loginName2"
data-win-bind="innerText: name; style.color: userType Tests.typeColorInitializer">
</span>
</p>
<img id="photo2" data-win-bind="src: photoURL"/>
</section>
```

Tip The syntax of data-win-bind is different than data-win-options! Whereas the options string is an object within braces { } with options separated by a comma, a binding string has no braces and items are separated by semicolons. If you find exceptions being thrown from Binding.processAll, check that you have the right syntax.

Here we're saying that the innerText property of the loginName2 target is bound to the source's name property and that the target's style.color property is bound to the source's userType property according to whatever relationship the Tests.typeColorInitializer establishes. As we'll see in a moment, that initializer is built directly around the userTypeToColor converter.

As you can see, the data-win-bind notation above does not specify the source object. That's the purpose of Binding.processAll. So, assuming we have a data source as before:

```
var login2 = { name: "liam", id: "12345678",
    photoURL: "http://www.kraigbrockschmidt.com/images/Liam07.png", userType: "kid"};
```

We call `processAll` with the target element and the source object as follows:

```
//processAll scans the element's tree for data-win-bind, using given object as data context
WinJS.Binding.processAll(document.getElementById("loginDisplay2"), login2);
```

**The data context** The second argument to `Binding.processAll` is the data context with which to perform the binding. If you omit this, it defaults to the global JavaScript context. If, for example, you have a namespace called `Data` that contains a property `bindSource`, you can specify `Data.bindSource` in `data-win-bind` and omit a context in `processAll`, or you can specify just `bindSource` in `data-win-bind` and pass `Data` as the second argument to `processAll`.

**Other arguments** `Binding.processAll` performs a deep traversal of all elements contained within the given root, so you need only call it once on that root for all data binding in that part of the DOM. If you want to process only that element’s children and not the root element itself, pass `true` as the third parameter (called `skipRoot`). A fourth parameter called `bindingCache` also exists as an optimization for holding the results of parsing data-win-bind expressions. Both `skipRoot` and `bindingCache` are useful when working with binding templates that we’ll talk about toward the end of this chapter.

The result of all this, in Test 2, is identical to what we did manually in Test 1. In fact, `processAll` basically takes the declarative `data-win-bind` syntax along with the source and target and dynamically executes the same code that we wrote out explicitly in Test 1. The one added bit is that the initializer function must be globally accessible and marked for processing, which is done as follows:

```
//Use a namespace to export function from the current module so WinJS.Binding can find it
WinJS.Namespace.define("Tests", {
    typeColorInitializer: WinJS.Binding.converter(userTypeToColor)
});
```

As with control constructors defined with `WinJS.Class.define`, `WinJS.Binding.converter` automatically marks the function it returns as safe for processing. It does a few more things as well, but we’ll return to that subject in a bit.

We could also put the data source object and applicable initializers within the same namespace.⁵² For example, in Test 3 we place our `login` data object and the `typeColorInitializer` function in a `LoginData` namespace, and the markup and code now look like this:

```
<section id="loginDisplay3">
    <p>You are logged in as
        <span id="loginName3"
              data-win-bind="innerText: name; style.color: userType LoginData.typeColorInitializer">
        </span>
```

⁵² More commonly, initializers and converters would be part of a namespace in which applicable UI elements are defined, because they’re more specific to the UI than to a data source.

```
</p>
<img id="photo3" data-win-bind="src: photoURL" />
</section>
```

```
WinJS.Binding.processAll(document.getElementById("loginDisplay3"), LoginData.login);

WinJS.Namespace.define("LoginData", {
  login : {
    name: "liam", id: "12345678",
    photoURL: "http://www.kraigbrockschmidt.com/images/Liam07.png",
    userType: "kid"
  },
  typeColorInitializer: WinJS.Binding.converter(userTypeToColor)
});
```

In summary, for one-time binding WinJS.Binding simply gives you a declarative syntax to do exactly what you'd do in code, with a lot less code. Because it's all just some custom markup and a processing function, there's no magic here, though such useful utilities are magical in their own way! In fact, the code here is really just one-way binding without having the source fire any change events. We'll see how to do that with WinJS.Binding.as in a moment after a couple more notes.

First, Binding.processAll is actually an async function that returns a promise. Any completed handler given to its then/done method will be called when the processing is finished, if you have additional code that's depending on that state.

Second, you can call Binding.processAll more than once on the same target element, specifying a different source object (data context) each time. This won't replace any existing bindings, mind you—it just adds new ones, meaning that you could end up binding the same target property to more than one source, which could become a big mess. So again, a better approach is to combine those sources into a single object and bind to that, using dot notation to identify nested properties.53

Third, the binding that we've created with WinJS here is actually one-way binding by default, not one-time, because one-way binding is the most common scenario. To get true one-time binding, use the built-in initializer function, oneTime, in your data-win-bind string. More on this under Binding Initializers later on.

## Sidebar: Additional Property Syntax and Binding to WinJS Controls

Property identifiers in data-win-bind can be single identifiers like name or compound identifiers such as style.color. This applies to both source and target properties. This is important when binding to properties of a WinJS control, rather than its root element, as those properties must be referenced through winControl. For example, if we had a source object called myData and

53 A final comment that only warrants a footnote is that in Windows 8, apps typically added a line of code WinJS.Binding.optimizeBindingReferences = true to avoid some memory leaks. This is done automatically in WinJS 2.0 (for Windows 8.1), so that line is no longer necessary.

wanted to bind some of its properties to those of a WinJS.UI.Rating control, we'd use the following syntax:

```
<div id="rating1" data-win-control="WinJS.UI.Rating"
 data-win-options="{onchange: changeRating}"
 data-win-bind="winControl.averageRating: myData.average; winControl.userRating: myData.rating">
</div>
```

Notice that data-win-control, data-win-options, and data-win-bind can be used together and UI.processAll() and Binding.processAll() will pick up the appropriate attributes. It's important, however, that UI.processAll() has completed its work before calling Binding.processAll() as the latter depends on the control being instantiated. Typically, then, you'll call Binding.processAll() within the completed handler for UI.processAll():

```
args.setPromise(WinJS.UI.processAll()).then(function () {
    WinJS.Binding.processAll(document.getElementById('boundElement'));
});
```

Within data-win-bind, array lookup for source properties using [ ] is not supported, though you can do that through an initializer. Array lookup is supported on the target side, as is dot notation. Also, if the target object has a property that you want to refer to using a hyphenated identifier (where dot notation won't work), you can use the following syntax:

```
<span data-win-bind="this['hyphenated-property']: source"></span>
```

That is, the target property string in data-win-bind basically carries through into the binding code that Binding.processAll generates; just as you can use this['hyphenated-property'] in code (this being the data context), you can use it in data-win-bind.

A similar syntax is necessary for binding attributes of the target element, such as the aria-* attributes for accessibility. As you probably know, attributes aren't directly accessible through JavaScript properties on an element: they're set through the element.setAttribute method instead. So you'd need to insert a converter into the data binding process to perform that particular step. Fortunately, WinJS.Binding includes initializers that do exactly this, initializer, setAttribute (for one-way binding) and setAttributeOneTime (for one-time binding). These are used as follows:

```
<label data-win-bind="this['aria-label']: title WinJS.Binding.setAttribute"></label>
<label data-win-bind="this['aria-label']: title WinJS.Binding.setAttributeOneTime"></label>
```

## One-Way Binding

The goal for one-way binding is, again, to update a target property, typically in a UI control, when the bound source property changes. One-way binding means to effectively repeat the one-time binding process whenever the source property changes.
