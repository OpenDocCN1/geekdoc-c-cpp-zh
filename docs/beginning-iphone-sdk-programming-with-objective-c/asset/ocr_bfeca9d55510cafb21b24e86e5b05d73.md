The main.m file contains code that bootstraps your application. It contains the following code, and you rarely need to modify it:

```
#import <UIKit/UIKit.h>

int main(int argc, char *argv[]) {
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    int retVal = UIApplicationMain(argc, argv, nil, nil);
    [pool release];
    return retVal;
}
```

Most of the hard work is done by the UIApplicationMain() function, which examines the Info.plist file to obtain more information about the project. In particular, it looks at the main nib file you will use for your project. Figure 3-3 shows the content of the Info.plist file. Notice that the Main nib file base name key is pointing to MainWindow, which is the name of the NIB file to load when the application is started.

# WHAT DO XIB AND NIB STAND FOR?

In your journey of iPhone application development, you will always come across files with the .xib extension (sometimes also known as NIB files). So, what do the NIB and .xib stand for, exactly? To understand this, a little history lesson is in order. Turns out that the current Mac OS X was built upon an operating system called NeXTSTEP, from a company known as NeXT (founded by Apple's cofounder, Steve Jobs, in 1985). The N in NIB stands for NeXTSTEP. As for xib, the x in presumably stands for XML, because its content is saved as an XML file. The IB stands for Interface Builder, the application that allows you to visually construct the UI for your application.

![](bbox=[0.1, 0.78, 0.75, 0.9])

FIGURE 3-3

# Editing XIB Files

Double-click the MainWindow.xib file to edit it using Interface Builder. As mentioned, the XIB file represents the UI of your application, and it is used almost exclusively by Interface Builder.