+   c. Connect the `emailField` outlet to the interface by Control-dragging from `InternetController` to the `NSTextField` in the main window of your interface.

+   d. Click `Connect` in the `Identity Inspector` window to make the connection.

+   6. Click the `InternetController` class and then choose `File ⇄ Write Class Files` to create and add the class files in Xcode.

+   7. Return to Xcode and change this line in `InternetController.h`:

```
```@interface InternetController : /* Specify a superclass (eg: NSObject or NSView) */ {```
```

to this

```
```@interface InternetController : NSObject {```
```

![](bbox=[0.24, 0.41, 0.73, 0.8])

**Figure 15-9:** Add two actions and one outlet to the Internet Controller class for the e-mail functions.