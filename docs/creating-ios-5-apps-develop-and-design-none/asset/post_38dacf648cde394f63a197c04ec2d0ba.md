
To check if a class is available, we simply call `[<class name> class]`. If this returns nil, the class is not available. To see if a method is available, we simply call the object's `respondsToSelector:` method. To see if a function is available, check to see if the function's name evaluates to NULL.

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

Unfortunately, the `[<class name> class]` test is only available if the base SDK is 4.2 or greater, and if the deployment target is 3.1 or greater. So if you're supporting iOS 3.0, you need to use a more verbose test.

```
Class cls = NSClassFromString(@"UIDocument");
if (cls) {
    // We can use the document.
} else {
    // We still have to use old-school file I/O.
}
```

Additionally, if you're going to be developing for earlier devices, you will need to download the debugging support. Select Xcode > Preferences from the main menu. Switch to the Downloads tab and download the required components.

On the surface, this is amazing. It means we can have our cake and eat it too. We can support old iOS 3.0 phones while also on newer devices enabling the newest iOS 5 features, like iCloud storage and Core Location regions. However, there is one huge problem here. There is no way to check the code at compile time and verify that we aren't accidentally calling something above the deployment target in a generally reachable branch.

Things aren't so bad when you're just adding a new feature to an existing app. You know that the code you're adding is above the deployment target, and you can take care to isolate it properly. The real problem comes in when you're doing general coding or debugging. It's so easy to unknowingly use parts of the SDK that are above the deployment target—especially when using autocomplete.

Unfortunately, there's only one way to catch these errors: testing. Sure, I like testing. I'm a huge fan of testing, but testing alone is not a sufficient solution for this problem. Here's the hard, cold truth: It's very hard (I would say impractical if not impossible) to make sure that we actually execute every possible branch of our code during our test cycles. And if we don't test every branch, we don't really know if we're safe. Above-deployment API calls may be scattered throughout any part of our code, lying in wait like little land mines, just waiting to kill our apps.

So, if you go down this route, test your code. Test it hard and test it often. If possible, find a bunch of beta testers who still run older versions of iOS. Otherwise, you're just asking for a bunch of bad reviews when your app starts crashing on older devices.

Finally, there are also some important limitations that weak linking just cannot work around. Storyboards, for example, are only available on iOS 5 and later. ARC is available for iOS 4.0 and above, but weak references are not supported before iOS 5. Therefore, if you want to support earlier devices, you must use nibs and manual memory management.

## LOCALIZATION

Localization involves adapting our application to two or more culturally distinct markets. People often think about localization in terms of translating written text—and it can involve a lot of translation. However, it also involves a wide range of other cultural aspects that have nothing to do with language. For example, we've already used NSNumberFormatter to create locally formatted numbers. There, it's not about language—we're not translating the number; we're simply choosing the best representation based on our user's locale. Similarly, a stop sign icon should look very different in Japan than it does in the US. Both of these are prime examples of localization.

- **genstrings**

This command-line utility can parse C and Objective-C files and can find all the keys declared using one of the `NSLocalizedString()` methods. It will then build the `.strings` files containing all the unique values it found. This file can then be sent to translators, and the translated versions can be placed in the appropriate language bundles.

Additionally, we don't need to translate every single string in our application. We only need to localize the strings that the user actually sees. Strings used as internal keys or as the names of notifications should be left alone.

For more information, see the Internationalization Programming Topics.

## ACCESSIBILITY

Recently, iOS has received a lot of praise and press for its excellent accessibility features. Out of the box, iOS provides a wide range of alternate input and output settings to assist people with low vision or blindness, hearing disabilities, and motor or physical disabilities. For the most part, these features are available to our application for free. We may need to be a little careful when creating custom gestures, since assistive touch won't support them, but other than that, we can focus all our attention on supporting VoiceOver.

For most standard controls, we just need to set the Accessibility settings in Interface Builder. These can be found in the Identity inspector. The label is a string that succinctly identifies the control. For example, "Units" or "Enter Weight."

The hint is a brief string that describes the effect of performing an action on the control. This should avoid mentioning either the control or the action. For example, "enter a new weight" not "select this text field to enter a new weight."

This, however, is just the beginning. iOS accessibility support provides a number of methods to help truly customize and refine the interface. I highly recommend reading through the Accessibility Programming Guide for iOS for more information.

## FILE SHARING

As we have seen, iOS 5 added document sharing using iCloud. However there are some older file sharing techniques we can still use. Even in the age of iCloud, these techniques have important roles to play.

For example, adding the UIFileSharingEnabled key to our application's Info.plist and setting its value to YES shares our application's Document directory with iTunes. From within iTunes, the user can see all the files in the Document directory. They can add new files and delete existing files.

This is still particularly useful if your users are likely to load a number of large files. Over-the-wire transfers from iTunes are still the fastest way to get large amounts of data onto our device. Furthermore, documents shared this way do not take up space in iCloud storage (though they may take up space in iCloud backup, depending on how the device is configured).

Applications can also transfer documents among themselves. To transfer a document to other applications, simply create an instance of UIDocumentInteractionController. Then call either `presentOpenInMenuFromBarButtonItem:animated:` or `presentOpenInMenuFromRect:inView:animated:`, depending on whether you want to anchor the menu to an arbitrary rectangle or to a bar button.

```objc
- (IBAction) exportButtonPressed:(id)sender {
    // Open file in other apps.
    UIDocumentInteractionController* controller =
        [UIDocumentInteractionController interactionControllerWithURL:
            fileURL];
    [controller presentOpenInMenuFromBarButtonItem:sender
                                        animated:YES];
}
```

The system will dynamically create a menu, listing all the applications that have registered support for the given document type.

The complement to this is, of course, that our applications can also register all the documents that they support. This requires two steps. First, add an appropriate document type to the target's Document Types list. We already did this in the "Preparing the Application" section of Chapter 6, when we registered our Health.
