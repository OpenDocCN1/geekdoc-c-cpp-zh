# # FILE SHARING

As we have seen, iOS 5 added document sharing using iCloud. However there are some older file sharing techniques we can still use. Even in the age of iCloud, these techniques have important roles to play.

For example, adding the UIFileSharingEnabled key to our application’s Info.plist and setting its value to YES shares our application’s Document directory with iTunes. From within iTunes, the user can see all the files in the Document directory. They can add new files and delete existing files.

This is still particularly useful if your users are likely to load a number of large files. Over-the-wire transfers from iTunes are still the fastest way to get large amounts of data onto our device. Furthermore, documents shared this way do not take up space in iCloud storage (though they may take up space in iCloud backup, depending on how the device is configured).

Applications can also transfer documents among themselves. To transfer a document to other applications, simply create an instance of UIDocumentInteractionController. Then call either presentOpenInMenuFromBarButtonItem:animated: or presentOpenInMenuFromRect:inView:animated:, depending on whether you want to anchor the menu to an arbitrary rectangle or to a bar button.

```
~~~objc
- (IBAction) exportButtonPressed:(id)sender {
    // Open file in other apps.
    UIDocumentInteractionController* controller =
        [UIDocumentInteractionController interactionControllerWithURL:
            fileURL];
    [controller presentOpenInMenuFromBarButtonItem:sender
                                        animated:YES];
}
~~~
```

The system will dynamically create a menu, listing all the applications that have registered support for the given document type.

The complement to this is, of course, that our applications can also register all the documents that they support. This requires two steps. First, add an appropriate document type to the target’s Document Types list. We already did this in the “Preparing the Application” section of Chapter 6, when we registered our Health