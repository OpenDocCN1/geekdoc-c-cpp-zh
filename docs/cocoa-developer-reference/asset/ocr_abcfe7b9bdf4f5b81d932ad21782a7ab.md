Figure 6.5 shows the `setTitle:` entry. It has a title followed by a brief description, followed by a code signature. Making sense of the signature is a fundamental skill. Even if you have experience in other object-oriented languages and already understand what each element does, some of the Objective-C syntax may be unfamiliar.

# Figure 6.5

The `setTitle:` method description includes a terse list of the method's features. Very few of the class reference pages include sample code or examples.

![](bbox=[0.198, 0.278, 0.837, 0.645])

# Understanding signatures

In this example, you want to send the `setTitle:` message to an instance of `NSWindow`. The signature tells you four things:

+   - The initial “-” character indicates that this is an instance method, not a class method. It must be run on an instance of `NSWindow`, not on the class as a whole. This is good news — it means you can use this method on `window`. For a class method, the initial character would be a “+,” and it would have to be run on `NSWindow` itself, not on an instance.