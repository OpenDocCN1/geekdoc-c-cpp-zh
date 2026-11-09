![](bbox=[0.18, 0.106, 0.214, 0.142])

# Joe Asks…

# **How Would I Have Known to Add the WebKit Framework?**

Start by opening the debugger with either Run > Debugger or ⇧⌘Y. Depending on how you’ve configured Xcode, you may also see an icon that looks like bug spray that you can click. In the top-left corner of your Xcode window, you will see the warning that the application is

```
TERMINATING DUE TO UNCAUGHT_EXCEPTION
```

The stack trace isn’t very helpful, but if you look at the Console, you will see the problem pretty quickly. Open the Console using ⇧⌘R or Run > Console. You’ll see a gdb prompt. Scroll back past a listing of the stack. Just above this you will see a series of lines that each begin with a time stamp, the word SimpleBrowser, and brackets around an identifier that includes the process number. Once you parse away all of this information, you should be left with something like this:

```
An uncaught exception was raised
-[NSKeyedUnarchiver decodeObjectForKey:]
        cannot decode object of class (WebView)
Terminating app due to uncaught exception
        'NSInvalidArgumentException'
```

A-ha! The problem is with unarchiving a WebView object. Your nib is essentially an archive of objects and their connections. You need to load the WebKit framework so that the WebView can be successfully reconstituted.

that can come up. See the *Joe Asks…* on this page for an explanation of how you might have diagnosed the problem yourself.

When we dragged the WebView instance from our library, we saw that it is part of the WebKit framework but not part of the Cocoa framework. I would have assumed that Xcode would automatically have added the WebKit framework to the corresponding project to link against, but it doesn’t. You need to do that yourself.

From the project view, select the Frameworks folder in the SimpleBrowser group. You should see four frameworks have already been added to the project, but if you look at the rightmost column, you’ll see that only Cocoa.framework is active for our target.