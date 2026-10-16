# Declaring an object that must implement a protocol

When declaring an instance variable that is expected to implement a given protocol, typically you use the id datatype so that any object can be stored in the variable. If you want to have the compiler verify that the required protocol methods are in fact implemented on whatever object you are actually storing in the variable, then you must also tell this to the compiler by specifying the protocol type information along with the datatype. To do this, in addition to the id datatype, you also specify the protocol you expect the object to adhere to after the id keyword, in angle brackets, as shown in Listing 7.5.

Listing 7.5

# Declaring a variable which implements a specific protocol

```
id<NetworkClient> *delegate;
```

In this case, the delegate object is being defined as adopting the NetworkClient protocol, and thus will be expected, by the compiler, to implement the appropriate required methods from that protocol.

Anywhere you are expected to declare a variable datatype, you can use this syntax. This includes method declarations, variable declarations, return types, and so on.

# NOTE

In those rare cases where you have not declared that your variable must implement a specific protocol, but you do require it, you can force the compiler to assume that a given object does implement a given protocol by typecasting it. To typecast a given variable to a given protocol, you actually typecast it to (id<SomeProtocol>). This isn’t required if you specify your protocols as part of your variable declarations, as is generally recommended.

# Exploring formal and informal protocols

I’ve mentioned it briefly before, but it bears further discussion here before we deal with how you handle optional methods.

There are, in fact, two different kinds of protocols, formal and informal. Informal protocols are the older style of protocols that are still used in part of cocoa and Objective-C. Informal protocols do not require a formal protocol declaration as I’ve shown you so far in this chapter. Informal protocols are typically declared as categories on the NSObject class. I discuss categories in the next chapter, so I won’t go into a great amount of detail here.

Because of the greater type safety that formal protocols provide and because of the fact that formal protocols have the @optional keyword that enables you to selectively mark individual methods as optional, generally speaking, formal protocols are the preferred way to create new protocols in your code.