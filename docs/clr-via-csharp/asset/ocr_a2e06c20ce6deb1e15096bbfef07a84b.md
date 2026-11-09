Both C# and the CLR allow for covariance and contra-variance of reference types when binding a method to a delegate. Covariance means that a method can return a type that is derived from the delegate's return type. Contra-variance means that a method can take a parameter that is a base of the delegate's parameter type. For example, given a delegate defined like this:

```
```csharp
delegate Object MyCallback(FileStream s);
```
```

it is possible to construct an instance of this delegate type bound to a method that is prototyped like this:

```
```csharp
String SomeMethod(Stream s);
```
```

Here, `SomeMethod`'s return type (`String`) is a type that is derived from the delegate's return type (`Object`); this covariance is allowed. `SomeMethod`'s parameter type (`Stream`) is a type that is a base class of the delegate's parameter type (`FileStream`); this contra-variance is allowed.

Note that covariance and contra-variance are supported only for reference types, not for value types or for `void`. So, for example, I cannot bind the following method to the `MyCallback` delegate:

```
```csharp
Int32 SomeOtherMethod(Stream s);
```
```

Even though `SomeOtherMethod`'s return type (`Int32`) is derived from `MyCallback`'s return type (`Object`), this form of covariance is not allowed because `Int32` is a value type. Obviously, the reason why value types and `void` cannot be used for covariance and contra-variance is because the memory structure for these things varies, whereas the memory structure for reference types is always a pointer. Fortunately, the C# compiler will produce an error if you attempt to do something that is not supported.

# ## Using Delegates to Call Back Instance Methods

I just explained how delegates can be used to call static methods, but they can also be used to call instance methods for a specific object. To understand how calling back an instance method works, look at the `InstanceDelegateDemo` method that appears in the code shown at the beginning of this chapter.

Notice that a `Program` object named `p` is constructed in the `InstanceDelegateDemo` method. This `Program` object doesn't have any instance fields or properties associated with it; I created it merely for demonstration purposes. When the new `Feedback` delegate object is constructed in the call to the `Counter` method, its constructor is passed `p.FeedbackToFile`. This causes the delegate to wrap a reference to the `FeedbackToFile` method, which is an instance method (not a static method). When `Counter` calls the callback method identified by its `fb` argument, the `FeedbackToFile` instance method is called, and the address of the