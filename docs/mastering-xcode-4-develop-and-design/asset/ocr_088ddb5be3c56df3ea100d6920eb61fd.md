The debugger calls the URL object’s -scheme method, then calls the returned object’s -description and prints this:

```
http
```

The information you see in the examples isn’t particularly exciting, but it can be enough to differentiate two similar objects inside a printed NSArray or NSDictionary object. While many objects in the Cocoa API come with reasonably useful descriptions, it’s up to the developer to override -description in their own objects and provide meaningful descriptions for their own debugging.

# PRINTING VALUES

The po command works only on objects. What about values of primitives? What if you wanted to know the length of the string returned by the URL object’s scheme for some reason? You might expect the following command to work:

```
po [[googleURL scheme] length]
```

It won’t work because the -length method of NSString returns an NSUInteger—a primitive type, not an object. For primitive values, you use a different print command.

```
p (NSUInteger)[[googleURL scheme] length]
```

The debugger responds with this:

```
$1 = 4
```

There certainly are four characters in the string http. Let’s take a quick look at the structure of the command and its response.

The command p (short for print) expects the result of the statement you give it to evaluate ([[googleURL scheme] length]) to be cast to the expected type (NSUInteger) so it knows how to represent it. This type should be the return type of the method or function that ultimately returns the value (the outermost call in nested calls). In the case of NSString’s -length method, that’s an NSUInteger.