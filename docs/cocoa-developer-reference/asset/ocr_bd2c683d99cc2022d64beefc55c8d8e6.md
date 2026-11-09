```
```objc
- (void) thisMethodDoesNothing {
} //Add these two lines to the method body list in the
implementation
```
```

The rules for defining parameter lists and return values are similar to those in C. Methods can take any number of parameters. Parameter types must be explicit. For example:

```
```objc
//This line appears in the interface
- (AClass *) thisMethodDoesSomething: (AnotherClass *)
aParameter;
//This block of code appears in the implementation
- (AClass *) thisMethodDoesSomething: (AnotherClass *) aParameter
{
AClass *aResult; //This is a private variable for this method
aResult = [aParameter doSomethingToIt];
return aResult;
}
```
```

![](bbox=[0.103, 0.414, 0.172, 0.47])

# TIP

aParameter is used as a private variable within the method. Name conflicts are common, so it can be useful to prefix parameters with an underscore to ensure that local parameter names don’t conflict with global properties.

```
```objc
- (AClass *) thisMethodDoesSomething:
(UsingAnotherClass *) _aParameter;
```
```

Xcode assumes that if your code references a method, it exists. If the compiler can’t find the method at compile time, it logs a warning but allows the build to complete. The compiler generates the same warning if you use a method before you define its implementation.

Method names are only loosely linked to objects, and the Objective-C run time looks up method names dynamically. For example, as long as aMethod is available in both classes, this is valid code even if both implementations of aMethod are different:

```
```objc
aPointer = anInstanceOfAClass;
[aPointer aMethod];
aPointer = anInstanceOfASubclassOfAClass;
[aPointer aMethod];
```
```

![](bbox=[0.103, 0.752, 0.172, 0.806])

# CAUTION

By default, when you create a new project, Xcode assumes you’ll be managing memory manually. Usually you’ll want to enable garbage collection instead. For instructions on how to do this, see the last section in Chapter 12. Projects in the rest of this book assume that garbage collection is enabled.