# Advanced Data-Binding Scenarios

Earlier in this chapter, you learned about the templating engine of the Microsoft Ajax Library, and how to display data on the client. All the examples demonstrated one-time, one-way bindings. The template was evaluated only once, and the data was rendered when the page loaded, or when an event was raised. When the data was modified by a client-side script, the page was not updated. Fortunately, the Microsoft Ajax Library supports not only one-way, one-time bindings, but it is also capable of building a continuous connection between the data source and the controls on the UI.

# Live Binding

If one-time binding does not suit your needs because you want to automatically update the UI when the data changes, you must switch to live binding. Live binding requires that the template engine be notified when a value of a variable or a property changes. When the template engine receives these notifications, it refreshes the rendered.

The only problem is that the JavaScript itself does not support raising notifications when a value changes. Fortunately, a manual workaround is needed.

If you already looked into the Ajax Library or created custom client components, you have probably met the raisePropertyChanged method of the Sys.Component class to expose the setter to raise the propertyChanged event. However, your class will only fire it if it inherits from the Sys.Component, Sys.UI.Behavior, or Sys.UI.Control base class. With this approach, you can use a simple object array bound to a DataView control, which you would have to wrap it in a component to build your code using the propertyChanged event.

Fortunately, a new class in Ajax Library 4, Sys.Observer, drastically makes your life easier. The primary purpose of this class is to make any object observable by providing helper methods to modify the object. If you use these methods, the Sys.Observer class will take care of raising all the notification events.

To make the previous countries collection observable, all you have to do is call the Sys.Observer.makeObservable method:

```
Sys.Observer.makeObservable(countries);
```

The makeObserver function adds a bunch of methods to the target object that can be used to modify it in an observable manner. If the object is an array, additional modification methods are added as well.

For example, you can add a new item to the array that subscribers will be notified about by calling the insert method:

```
countries.insert(0, { Name: 'Switzerland', Capital: 'Bern' });
```

> Code file [3-AjaxLibrary\11-LiveBinding.htm] available for download at Wrox.com