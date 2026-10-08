+   2. Define the displayAsString method in MyTextController.m.

The code creates a string, someString, and then tells the textView to set its string to someString:

```
- (IBAction)displayAsString:(id)sender
{
  NSString* someString = @"Cocoa says hello!";
  [textView setString:someString];
}
```

+   3. Double-click the MainMenu.xib file to open the project’s interface in Interface Builder.

+   4. Add an NSButton to the window in your interface.

+   5. Change the button’s Title Attribute in the Inspector window to display NSString.

+   6. Control+drag from the button to the MyTextController instance and connect it to the displayAsString: action in the black connections list overlay that opens.

Notice that Interface Builder has read the MyTextController.h file on opening the interface and now an action named displayAsString: is available in MyTextController.

Replacing specific text is another task that you might want to perform. To replace some portion of the text in an NSTextView, you must first define an NSRange variable. This range describes which part of the string you want to replace. In the preceding example, you used the string "Cocoa says hello! ". If you want to change hello to goodbye, you’d first find the location of that word in the string. Because the numbering begins at 0, the first letter of hello is the 11th character in the string. Further, the length of hello is 5. Thus, to make an NSRange for hello, you’d use code like this:

```
NSRange theRange;
theRange = NSMakeRange(11, 5);
```

To replace hello with goodbye, call the replaceCharactersInRange method of the NSTextView:

```
[textView replaceCharactersInRange:theRange
withString:@"Goodbye" ];
```

Besides editing the text, you’ll sometimes want to programmatically select portions of the text in an NSTextView. For example, suppose you want to perform a Select All operation. Create an NSRange representing the entire length of the text and then call the setSelectedRange method of the NSTextView to select the text: