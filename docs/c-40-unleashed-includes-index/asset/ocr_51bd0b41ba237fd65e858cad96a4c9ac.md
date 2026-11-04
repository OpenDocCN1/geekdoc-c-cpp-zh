```
```csharp
private PaymentService()
{
    // This is a private constructor; therefore it can only
    // be called from inside the PaymentService type.
    _payments = new Queue<Payment>();
}
```
```

They look like methods but lack a name or a return type, depending on your point of view. One way to look at it is as a method whose name is the same as the containing class’s. Alternatively, you could say it doesn’t have a name and the return type is the containing class.

Because there’s no static keyword on the preceding constructor, it’s an instance constructor, which can be called using the new keyword, as we see in the Service property. Because it’s declared with the private access modifier, the only valid place for it to be called is from inside the same class. Notice that the constructor does initialize per-instance state that’s kept in the _payments field. The underscore-prefixed notation is a widely used pattern to recognize the use of fields rather than, say, local variables or parameters.

```
```csharp
private Queue<Payment> _payments;
```
```

The Service property is declared as public and static, hence the way to call it will be as follows, “dotting into the type”:

```
```csharp
PaymentService theOneAndOnlyInstance = PaymentService.Service;
```
```

On the inside, this property checks whether there’s already a single instance of the type created by checking the static s_service field. Across all instances of the type, there’ll be only one such field, which is exactly what allows us to enforce the singleton policy:

```
```csharp
public static PaymentService Service
{
    get
    {
        // Create service the first time it's requested. For
        // the remainder of the program's lifetime we'll be
        // using this singleton instance.
        if (s_service == null)
        {
            s_service = new PaymentService();
        }

        return s_service;
    }
}
```
```