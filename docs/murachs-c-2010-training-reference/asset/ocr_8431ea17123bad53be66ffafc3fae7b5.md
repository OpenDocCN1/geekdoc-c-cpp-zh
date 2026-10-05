# Chapter 13 How to work with indexers, delegates, events, and operators 405

The syntax for declaring an event
public event Delegate EventName;

# Code that declares and raises an event in the ProductList class

```
public class ProductList {
    public delegate void EventHandler(ProductList products);
    public event EventHandler Changed; // Declare the event

    public void Add(Product product) {
        products.Add(product);
        Changed(this); // Raise the event
    }
}
```

# Code that uses a named method to handle the event

```
ProductList products = new ProductList();

// Wire the event to the method that handles the event
products.Changed += new ProductList.EventHandler(OnChange);

// Handle the event
private void HandleChange(ProductList products) {
    products.Save();
    FillProductListBox();
}
```

# Code that uses an anonymous method to handle an event

```
// Wire the event to the anonymous method that handles the event
products.Changed += delegate(ProductList products) {
    products.Save();
    FillProductListBox();
}
```

# Description

+   - An event is a signal that an action has occurred on an object that was created from the class. To create an event that can be used by other classes, the event must be declared with public access at the class level. Then, the event can be called from any properties or methods that need to raise the event.
- An event declaration specifies a delegate that will handle the event along with the name.
- To raise the event, you refer to it by its name, and you code the arguments required by the delegate.
- To handle an event from another class, you create an instance of the class that raises the event and assign it to a class variable. Then, you declare an event handler that matches the event's signature. Finally, you wire the event to the event handler in the class constructor or, if the class is a form, in the Load event handler.

Figure 13-6 How to define and use events