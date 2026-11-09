ing a search for a given string that is not case sensitive in the forward direction with wrapping enabled.

Your Cocoa code should be readable. A month after you’ve written a method, you should be able to quickly reconstruct your intent and understand what the method does. In WebView, you can see the method `moveToBeginningOfSentenceAndModifySelection:`. The name of a method might be longer than its implementation—but what the method does is immediately clear to anyone who invokes it in code or connects to it using Interface Builder.

You’ll find more information about methods in the “Objects, Classes, and Messaging” chapter of Apple’s *The Objective-C Programming Language* [App09]. There’s also a nice entry on Stack Overflow about passing multiple parameters in Objective-C.⁵ You should also check out Apple’s *Coding Guidelines for Cocoa* [App06] for guidelines on naming methods. Matt Gallagher has a nice post on Cocoa with Love about method names.⁶

# 3.4 Dynamic Binding

Let’s take a look behind the scenes at what happens when an Objective-C message is sent. The simplest of cases, as shown here:

```
`[myWebView goBack]`
```

is converted at runtime to the following function call:

```
`objc_msgSend(myWebView, goBack)`
```

The receiver is passed in as the first argument and the selector as the second. The more complicated message, as shown here:

```
`[myWebView searchFor:myString direction:YES caseSensitive:NO wrap:YES]`
```

is converted at runtime to this function call:

```
`objc_msgSend(myWebView, searchFor:direction:caseSensitive:wrap:, myString, YES, NO, YES)`
```

Again, the receiver is passed in as the first argument, and the selector is passed in as the second. The parameters are passed in as the remaining function arguments.

+   5. http://stackoverflow.com/questions/722651/how-do-i-pass-multiple-parameters-in-objective-c
+   6. http://cocoawithlove.com/2009/06/method-names-in-objective-c.html