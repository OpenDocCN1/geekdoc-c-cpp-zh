
In the previous section's code, if we changed `login.name` after calling `Binding.processAll`, nothing will change in the output UI. So how can we automatically update the output?

Generally speaking, this requires that the data source maintains a list of `bindings`, where each binding describes a source property, a target property, and any associated converter function. The data source also needs to provide methods to manage that list, like `addBinding`, `removeBinding`, and so forth. Thirdly, whenever one of its bindable properties changes it goes through its list of bindings and updates any affected target property accordingly. All together, this makes what we call an *observable source*.

These requirements are quite generic; you can imagine that their implementation would pretty much join the ranks of classic boilerplate code. So, of course, `WinJS.Binding` provides just such an implementation with two functions at its core!

- `Binding.as` wraps any arbitrary object with an observable structure. (It’s a no-op for nonobjects, and `Binding.unwrap` removes that structure if there’s a need.)
- `Binding.define` creates a constructor for observable objects around a set of properties (described by a kind of empty object that just has property names). Such a constructor allows you to instantiate source objects dynamically, as when processing data retrieved from an online service.

Let’s see some code. Going back to the last BindingTests example above (Test 3), any time before or after `Binding.processAll` we can take the `LoginData.login` object and make it observable with just one line of code:

```
var loginObservable = WinJS.Binding.as(LoginData.login)
```

With everything else the same as before, we can now change a bound property within the `loginObservable` object:

```
loginObservable.name = "liambro";
```

This will update the target property (the mechanics of which we’ll talk about under “Under the Covers: Binding mixes” a little later):

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_287_0.png)

Here’s how we’d then create and use a reusable class for an observable object (Test 4 in the BindingTests example). Notice the object we pass to `Binding.define` contains property names, but no values (they’ll be ignored in any case):

```javascript
WinJS.Namespace.define("LoginData", {
    //...

    // LoginClass is a constructor for observable objects with the specified properties
    LoginClass: WinJS.Binding.define({name: "", id: "", photoURL: "", userType: "" }),
});
```

We can now create instances of LoginClass, initializing desired properties with values. In this example, we’re using a different picture and leaving userType uninitialized:

```javascript
var login4 = new LoginData.LoginClass({ name: "liamb",
    photoURL: "http://www.kraigbrockschmidt.com/images/Liam08.png" });
```

Binding to this login object, the username initially comes out black.

```javascript
//Do the binding (initial color of name would be black)
WinJS.Binding.processAll(document.getElementById("loginDisplay"), login4);
```

Updating the userType property will then cause an update the color of the target property, which happens through the converter automatically. In the example, this line of code is executed after a two-second delay so that you can see it change when you run the app:

```javascript
login4.userType = "kid";
```

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_288_0.png)

## Sidebar: Binding to WinRT Objects

Although it is possible to declaratively bind directly to WinRT source objects, those objects support only one-time binding. The underlying reason for this is that each WinRT object is represented in JavaScript by a thin proxy that’s linked to that object instance, but calling WinJS.Binding.as on this proxy does not make the WinRT observable within the rest of the WinJS bindings mechanisms. For this reason, it’s necessary to enforce one-time binding when using such sources directly. This can be done by specifying the WinJS oneTime initializer within each data-win-bind relationship, or specifying oneTime as the default initializer for processAll (the fifth argument). For example:

```javascript
WinJS.Binding.processAll(element, winRTSourceObject, false, null, WinJS.Binding.OneTime);
```

As in the previous sidebar, if you’re binding to element attributes, you’ll need to use the `setAttributeOneTime` initializer instead.

To work around this limitation, you can create a custom proxy in JavaScript that watches changes in the WinRT source and copies those values to properties in the proxy. Because this proxy has its own set of properties, you can then make it observable with `WinJS.Binding.as`.

## Implementing Two-Way Binding

As mentioned earlier, WinJS doesn’t presently include any facilities for two-way binding, but it’s straightforward to implement on your own:

- 1. Add listeners to the appropriate UI element events that relate to bound data source properties.
- 2. Within those handlers, update the data source properties.

The data source should be smart enough to know when the new value of the property is already the same as the target property, in which case it shouldn’t try to update the target lest you get caught in a loop. The observable object code that WinJS provides does this type of check for you.

To see an example of this, refer scenario 1 of the Declarative binding sample in the SDK, which listens for the change event on text boxes and updates values in its source accordingly. The input controls are declared as follows (`html/1_BasicBinding.html`, omitting much of the surrounding HTML structure):

~~~html
<input type="text" id="basicBindingInputText" />
<input type="text" id="basicBindingInputRed" />
<input type="text" id="basicBindingInputGreen" />
<input type="text" id="basicBindingInputBlue" />
~~~

and the output elements like so:

~~~html
<p>The text you entered was <span data-win-bind="innerHTML: text"></span>.
The value for red is <span data-win-bind="innerHTML: color.red"></span>,
the value for green is <span data-win-bind="innerHTML: color['green']"></span>,
and blue is <span data-win-bind="innerHTML: color.blue"></span>.
</p>
<p data-win-bind="style.backgroundColor: color.BasicBinding.ToCssColor">
And here’s your color as a background.</p>
~~~

The source object is defined in `js/1_BasicBinding.js` as a member of the surrounding page control:

~~~javascript
this.bindingSource = {
    text: "Initial text",
    color: {
        red: 128,
        green: 128,
        blue: 128
    }
};
~~~

and is made observable through this line of code:

```
var b = WinJS.Binding.as(this.bindingSource);
```

You can see how its members are referenced in the data-win-bind attributes above, so that when we call processAll (on the div that contains all the output element):

```
WinJS.Binding.processAll(element.querySelector("#basicBindingOutput"), this.bindingSource);
```

we've set up one-way binding between the data source and the output. To complete two-way binding, we set up event handlers for the change event of each input field that take the value from the control and copy it back to the observable source:

```
this.bindTextBox("#basicBindingInputText", b.text, function (value) { b.text = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputRed", b.color.red, function (value) { b.color.red = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputGreen", b.color.green, function (value) { b.color.green = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputBlue", b.color.blue, function (value) { b.color.blue = toStaticHTML(value); });
```

```
bindTextBox: function (selector, initialValue, setterCallback) {
var textBox = this.element.querySelector(selector);
textBox.addEventListener("change", function (evt) {
setterCallback(evt.target.value);
}, false);
textBox.value = initialValue;
}
```

In the HTML, you might have noticed an initializer called BasicBinding.toCssColor. This is defined in js/1_BasicBinding.js as follows:

```
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
