In our example program, we put up a dialog box to ask the user whether it is OK to close the window (see Figure 10.51). If the user doesn’t agree, the window stays open.

![](bbox=[0.139, 0.217, 0.774, 0.541])

**Figure 10.51** The user can veto the close property.

Here is how you achieve such a notification.

+   1. Add a listener object to each frame. The object must belong to some class that implements the `VetoableChangeListener` interface. It is best to add the listener right after constructing the frame. In our example, we use the frame class that constructs the internal frames. Another option would be to use an anonymous inner class.

```
iframe.addVetoableChangeListener(listener);
```

+   2. Implement the `vetoableChange` method, the only method required by the `VetoableChangeListener` interface. The method receives a `PropertyChangeEvent` object. Use the `getName` method to find the name of the property that is about to be changed (such as "closed" if the method call to veto is `setClosed(true)`. You obtain the property name by removing the "set" prefix from the method name and changing the next letter to lower case.