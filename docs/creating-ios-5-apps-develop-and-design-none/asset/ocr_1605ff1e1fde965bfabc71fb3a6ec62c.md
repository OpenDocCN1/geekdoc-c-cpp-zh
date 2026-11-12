To check if a class is available, we simply call [<class name> class]. If this returns nil, the class is not available. To see if a method is available, we simply call the object's respondsToSelector: method. To see if a function is available, check to see if the function's name evaluates to NULL.

```
    if ([UIDocument class]) {
        // We can use UIDocument.
    } else {
        // We must use old-school file I/O.
    }

    if ([self respondsToSelector:
        @selector(childViewControllers)]) {
        // We can create a custom UIViewController container.
    }

    if (UIAccessibilityIsClosedCaptioningEnabled != NULL) {
        // The function is safe to use.
    }
```

Unfortunately, the [<class name> class] test is only available if the base SDK is 4.2 or greater, and if the deployment target is 3.1 or greater. So if you're supporting iOS 3.0, you need to use a more verbose test.

```
Class cls = NSClassFromString(@"UIDocument");
If (cls) {
    // We can use the document.
} else {
    // We still have to use old-school file I/O.
}
```

Additionally, if you're going to be developing for earlier devices, you will need to download the debugging support. Select Xcode > Preferences from the main menu. Switch to the Downloads tab and download the required components.

On the surface, this is amazing. It means we can have our cake and eat it too. We can support old iOS 3.0 phones while also on newer devices enabling the newest