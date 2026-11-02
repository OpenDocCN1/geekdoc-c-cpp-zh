values (they’ll be ignored in any case):

```
```javascript
WinJS.Namespace.define("LoginData", {
    //...

    // LoginClass is a constructor for observable objects with the specified properties
    LoginClass: WinJS.Binding.define({name: "", id: "", photoURL: "", userType: "" }),
});
```
```

We can now create instances of LoginClass, initializing desired properties with values. In this example, we’re using a different picture and leaving userType uninitialized:

```
```javascript
var login4 = new LoginData.LoginClass({ name: "liamb",
    photoURL: "http://www.kraigbrockschmidt.com/images/Liam08.png" });
```
```

Binding to this login object, the username initially comes out black.

```
```javascript
//Do the binding (initial color of name would be black)
WinJS.Binding.processAll(document.getElementById("loginDisplay"), login4);
```
```

Updating the userType property will then cause an update the color of the target property, which happens through the converter automatically. In the example, this line of code is executed after a two-second delay so that you can see it change when you run the app:

```
```javascript
login4.userType = "kid";
```
```

![](bbox=[0.141, 0.487, 0.299, 0.646])

# Sidebar: Binding to WinRT Objects

Although it is possible to declaratively bind directly to WinRT source objects, those objects support only one-time binding. The underlying reason for this is that each WinRT object is represented in JavaScript by a thin proxy that’s linked to that object instance, but calling WinJS.Binding.as on this proxy does not make the WinRT observable within the rest of the WinJS bindings mechanisms. For this reason, it’s necessary to enforce one-time binding when using such sources directly. This can be done by specifying the WinJS oneTime initializer within each data-win-bind relationship, or specifying oneTime as the default initializer for processAll (the fifth argument). For example:

```
```javascript
WinJS.Binding.processAll(element, winRTSourceObject, false, null, WinJS.Binding.OneTime);
```
```