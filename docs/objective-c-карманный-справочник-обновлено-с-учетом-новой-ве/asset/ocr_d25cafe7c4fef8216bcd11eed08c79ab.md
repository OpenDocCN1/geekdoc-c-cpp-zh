intentional. There is nothing in C that behaves the same way as an Objective-C message send, so having new syntax highlights the fact that you also have new semantics. Remember that Tom Love described it has a hybrid language, with a clear syntax separation between the pure C parts and “object land,” which has Smalltalk-like syntax to accompany Smalltalk-like semantics.

The simplest kind of message send takes no arguments. An example of this might be the -count message sent to an array. Note the minus sign before the message name. This is the convention used in Objective-C documentation to indicate a message that is sent to an instance. A plus sign is used to indicate a message sent to a class, such as +new or +arrayWithObject::

```
size = [anArray count];
```

This snippet gets the number of elements in an array and stores it in the variable size. In a language such as C++ or Java, the equivalent would be something like this:

```
size = anArray.size();
```

This same syntax in Objective-C would be used if anArray were a C structure and the size field were a function pointer. Because this means something very different to sending a message to an object, the designers thought it would be confusing to use the same syntax.

Messages that take one argument look very