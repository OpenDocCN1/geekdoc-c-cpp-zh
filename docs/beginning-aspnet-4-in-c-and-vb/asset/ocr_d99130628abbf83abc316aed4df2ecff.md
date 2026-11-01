```
```javascript
Sys.Application.add_load(LoadHandler);
function LoadHandler(sender, args)
{
    Sys.Debug.traceDump(sender);
}
```
```

This results in output along the lines of the following:

```
```
traceDump (Sys._Application)
    updating: false
    _id: null
    _disposing: false
    _creatingComponents: false
    _disposableObjects (Array)
    _components (Object)
    _createdComponents (Array)
    _secondPassComponents (Array)
    _loadHandlerDelegate: null
    _events (Sys.UI.EventHandlerList)
        _list (Object)
            load (Array)
                [0] (Function)
    _initialized: true
    _initializing: true
```
```

You can see all the properties of this object in this output. This technique can be extremely useful for ASP.NET AJAX development.

# Making Asynchronous Web Method Calls

One of the most powerful features of ASP.NET AJAX is the ability to call web methods from client-side script. This gives you access to data, server-side processing, and all manner of other functionality.

You will not be looking at web methods in this book until Chapter 43, “Windows Communication Foundation,” so we will save the details until then and cover the basics here. Put simply, a web method is a method that you can expose from a Web service that enables you to access remote resources over the Internet. In ASP.NET AJAX, you can also expose web methods as static methods of server-side web page code-behind code. You can use parameters and return values in web methods just as you do in other method types.

In ASP.NET AJAX, web methods are called asynchronously. You pass parameters to a web method and define a callback function, which is called when the web method call completes. You use this callback function to process the web method response. You can also provide an alternative callback function to call in the event of a call failure.

In the PCSLibraryDemo application, you can see a web method call being performed by clicking the Call Web Method button, as shown in Figure 41-20.

![](bbox=[0.15, 0.7, 0.75, 0.9])