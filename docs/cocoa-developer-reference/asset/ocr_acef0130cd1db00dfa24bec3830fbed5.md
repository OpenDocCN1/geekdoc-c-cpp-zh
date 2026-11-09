# Saving and loading rich text

If you save the text with this version of the editor, you’ll see that the styling information disappears. When you reload the text, the application applies the last selected styling to the entire file.

The original Picopad save/open code writes standard unattributed strings. To support attributes, save and load the file as rich text as shown below.

The open and save methods use the block structure introduced in Picopad, but the `RTFFromRange:` method is used to generate an RTF stream in an NSData object, which is saved to a file. The Open code is simpler. It uses the `readRTFFromFile:` method to read the RTF data back into the text view.

![](bbox=[0.119, 0.361, 0.188, 0.416])

> > **CAUTION**
> >
> > Note that both methods run on the text view, not on a separate attributed string property of the text view. They’re the same as methods used with `NSAttributedString`, but they’re part of the `NSText` class, which is Cocoa’s default text container object. `NSTextView` is a subclass of `NSText` and inherits its methods.

```
```objective-c
@implementation TheWindow
@synthesize theTextView;
- (void) awakeFromNib {
    //Nothing happens here.
    //You could add auto-load of the last saved file...
}
- (void) saveTheDocument: (id) sender {
    NSSavePanel *savePanel = [NSSavePanel savePanel];
    savePanel.allowedFileTypes = [NSArray arrayWithObject:@"rtf"];
    [savePanel beginSheetModalForWindow:self
                     completionHandler:^(NSInteger result) {
        if (result == NSFileHandlingPanelOKButton) {
            NSData *theData = [theTextView RTFFromRange:
                NSMakeRange(0, [theTextView.string length])];
            [theData writeToURL: savePanel.URL atomically: YES];
        }
    }];
}
- (void) openADocument: (id) sender {
    NSOpenPanel *openPanel = [NSOpenPanel openPanel];
    openPanel.allowedFileTypes = [NSArray arrayWithObject:@"rtf"];
    [openPanel beginSheetModalForWindow:self
                     completionHandler:^(NSInteger result) {
        if (result == NSFileHandlingPanelOKButton) {
            [theTextView readRTFFromFile: openPanel.URL.path];
        }
    }];
}
@end
```
```