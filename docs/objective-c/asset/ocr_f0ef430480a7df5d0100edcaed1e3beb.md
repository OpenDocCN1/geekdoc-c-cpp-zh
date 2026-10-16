Typically, you would only need to do this in cases where you did not specify the type of the protocol as part of the datatype for the variable in question. If you had specified the protocol is part of the datatype for the variable then the compiler would have flagged this variable for you if it did not implement the protocol required.

# NOTE

The -conformsToProtocol: method shown in Listing 7.6 only works with formal protocols. If you're using an informal protocol, use the NSObject method -respondsToSelector: as shown in Listing 7.7 instead.

Even when you are certain that a given object implements a given protocol, there is still the possibility that the object may not implement any of the optional methods of the protocol.

Remember, if an object does not implement an optional method and you call that method on that object, then your application will crash. Therefore, you need a way to determine if that object actually implements an optional method before you attempt to call it.

Fortunately, NSObject, which all objects inherit from, has a method which does exactly this. This method is -respondsToSelector: and it takes as a parameter a selector object.

Just like with the protocol object, a special directive can be used to convert a method signature into a selector object. That directive is the @selector() directive. Its use, along with the -respondsToSelector: method, is shown in Listing 7.7.

# Listing 7.7

# Testing to determine if an object implements an optional method

```
-(void)disconnected;
{
    if ([delegate respondsToSelector:@selector(networkConnectorDisconnected:)])
        [delegate networkConnectorDisconnected:self];

    // else implement some default behavior...
}
```

In this example, you first check to see if the object which implements the protocol in fact implements one of the optional methods using the call -respondsToSelector:. If it does, then it goes ahead and calls that method. If it does not, you can choose to either do nothing, or to implement some kind of default behavior instead.