```
```csharp
static void sayHello_KeyDownOrClick(object sender, EventArgs e) {
    // Common logic goes here, for example, using (Button)sender
}
```
```

Here we're using the rules that relate to method group conversion, which take contravariance into account. All this means is that it's possible to create a delegate (here used as an event handler) referring to method that has less-derived parameter types than the types that are expected. For example, although MouseMove expects a delegate to a method with a second argument typed as MouseEventArgs, it's fine to pass it a delegate to a method that takes in an EventArgs in the parameter position instead. To see why this is fine, simply think of what happens when the delegate gets invoked by the event source, passing in a MouseEventArgs. Through the delegate it will be passed on to the event handler method that accepts the parameter as an EventArgs object, which is fine because every MouseEventArgs is an EventArgs.

Where contravariance applies to parameter types, covariance applies to the return type but is rarely used in the context of event handlers (because those typically have a void return type). Co- and contravariance for delegate return types and parameter types is depicted in Figure 18.18. It helps to keep in mind the Latin-originating meaning of the prefixes co (with the flow) and contra (against the flow) when looking at the diagrams.

![](bbox=[0.18, 0.72, 0.82, 0.9])

FIGURE 18.18 · Co- and contravariance for delegate types.