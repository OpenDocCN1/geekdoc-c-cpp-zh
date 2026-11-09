# Using Key-Value Coding

Like selectors, Key-Value Coding (KVC) introduces direction into Objective-C. But KVC is a very different and unrelated technology, with very different applications.

KVC makes it possible to access properties indirectly, using their name strings.

```
aReturn = anObject.aProperty;                 //Direct access
aReturn = [anObject valueForKey: @"aProperty"]; //KVC access
```

KVC looks simple in theory, but it can be tricky in practice. Some of the issues include:

+   - **Values must be “objectified.”** The technology could more accurately be called Key-Object Coding, because, with a few exceptions, values must be wrapped inside objects.
+   - **KVC isn’t usually used for standard property access.** It’s easier to use standard setters, getters, and `@synthesize`.
+   - **KVC is widely used to initialize and return groups of values and to access the values in data collection objects.** You must master it to use Cocoa effectively.
+   - **Cocoa’s keypath management can seem erratic.** You can use `object.prop-erty.subproperty` syntax to define a keypath. But not all classes support keypath access, and classes that do support it don’t always implement it consistently. This particularly applies to mutable data collections.
+   - **KVC makes it harder to trap errors.** If you use string literals as keys, the compiler can’t check them. You can solve this problem by defining the key strings as constants in a header file and using them throughout your code.

# “Objectifying” values

Consider this simple example of KVC, which reads and sets some of the values of `NSWindow`. This code looks like a reasonable attempt to set the `hasShadow` property.

```
[window setValue: NO forKey: @"hasShadow"];
```

But it doesn’t work, because `setValue:` expects an object, not a BOOL. The correct code is:

```
[window setValue: [NSNumber numberWithBool: NO]
forKey: @"hasShadow"];
```

This demonstrates how values must be objectified, adding an extra layer of complexity to KVC. Figure 9.10 illustrates this.