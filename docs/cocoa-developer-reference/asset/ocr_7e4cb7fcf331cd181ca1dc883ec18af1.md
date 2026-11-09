# # Using Cocoa Design Patterns and Advanced Messaging

> > It’s traditional in a Cocoa book to mention design patterns and
> > features such as Model-View-Controller (MVC), target-action,
> > Key-Value Coding (KVC), and Key-Value Observing (KVO).

Apple’s documentation mystifies these design patterns and makes them seem more difficult and complex than they really are. They’re an essential part of Cocoa, and you can use them to implement impressively efficient code. But the practice can be much simpler than the theory.

# ## Understanding Model-View-Controller

Model-View-Controller, often shortened to MVC, was introduced in Chapter 2. The outline of MVC is shown in Figure 9.1. An application is split into three elements — a store of data called a model, an interface called a view, and a controller object that passes data between them.

MVC implies, but doesn’t enforce, the suggestion that model data should be kept in separate objects and perhaps in separate custom classes.

In a simple application, this seems unnecessarily complex, because it is. If your data is in a single array or dictionary, there’s nothing to be gained by taking a data object out of the App Delegate and putting it into a separate wrapper object. It can be useful in a larger application to keep data in a separate data-handling class. But generally, the key feature of MVC isn’t how the data is stored but how it’s processed and prepared for display by the controller.

+   **In This Chapter**
+   
+   - Understanding Model-View-Controller in Cocoa
+   - Understanding and using target-action
+   - Using Key-Value Coding
+   - Using Key-Value Observing
+   - Working with notifications and errors