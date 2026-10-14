# Lambda expressions and anonymous methods

Lambda expressions were added to the C# language in version 3.0. C# version 2.0 introduced anonymous methods, which can perform a similar task but are not as flexible. Anonymous methods were added primarily so that you can define delegates without having to create a named method—you simply provide the definition of the method body in place of the method name, like this:

Click here to view code image

```
this.stopMachinery += delegate { folder.StopFolding(0); };
```

You can also pass an anonymous method as a parameter in place of a delegate, like this:

Click here to view code image

```
control.Add(delegate { folder.StopFolding(0); });
```

Notice that whenever you introduce an anonymous method, you must prefix it with the delegate keyword. Also, any parameters needed are specified in parentheses following the delegate keyword, as illustrated in the following example:

Click here to view code image

```
control.Add(delegate(int param1, string param2)
    { /* code that uses param1 and param2 */ ... });
```

Lambda expressions provide a more succinct and natural syntax than anonymous methods, and they pervade many of the more advanced aspects of C#, as you will see throughout the subsequent chapters in this book. Generally speaking, you should use lambda expressions rather than anonymous methods in your code.

# Comparing arrays and collections

Here’s a summary of the important differences between arrays and collections:

+   - An array instance has a fixed size and cannot grow or shrink. A collection can dynamically resize itself as required.
+   - An array can have more than one dimension. A collection is linear. However, the items in a collection can be collections themselves, so you can imitate a multidimensional array as a collection of collections.
+   - You store and retrieve an item in an array by using an index. Not all collections support this notion. For example, to store an item in a List<T> collection, you use the Add or Insert method, and to retrieve an item, you use the Find method.