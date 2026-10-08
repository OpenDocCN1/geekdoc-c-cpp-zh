
The code for both actions works similarly, with a few exceptions:

- Both actions display a `SavePanel` so that users can select the name and destination of the file they want to save.
- The two methods differ on the file type and title that they display in the `SavePanel` and the fact that plain text files need an encoding.

To display the panel, each method uses this line of code:

```objective-c
if ([theSavePanel runModal] == NSOKButton)
```

The `runModal` method of the `SavePanel` takes care of displaying the modal window. A modal window is one in which users are forced into a mode of operation — they must make a decision (saving a file or halting the operation) before proceeding any further.

When a user clicks a file and clicks the Save button in the `SavePanel`, the `runModal` function of the `SavePanel` returns a value. Instead of worrying about what numerical value it returns, Cocoa provides you with the constant `NSOKButton` indicating that the user clicked the Save button. The following code example checks for the Save button. Conversely, you could check for the Cancel button by using the appropriate constant for that button:

```objective-c
if ([theSavePanel runModal] == NSCancelButton)
```

If the users click Save in the `SavePanel`, the code writes the text from the `TextView` to a plain or rich text file.

For plain text files, this means using the `writeToFile` method of the `NSString` class:

```objective-c
[[textView string] writeToFile: [savePanel filename]
 atomically: YES encoding: NSUTF8StringEncoding
 error: NULL];
```

You retrieve the text from the text view as an `NSString` using the `[textView string]` method. The text file is saved with the `writeToFile` method, passing it four parameters:

- The name of the file that the user entered in the `SavePanel`.
- A Boolean value titled `atomically:`. If you pass `YES` as the `atomically` parameter, the `writeToFile` method first writes the data to a temporary file and renames that file after the write operation is finished. If it has a value of `NO`, `writeToFile` writes the data directly to the file returned by the `filename` method. Set the `atomically` parameter to `YES`.
- An encoding: The encoding is best set to `UTF8`, as it accounts for languages beyond English.
- An error routine should something go wrong: The `error` parameter can be set to `NULL`, as I won’t trap errors in this demo.

The second method in the code listing saves the file to a rich text file. Much of the code in it is identical to the plain text version, with one big exception. Instead of retrieving text from text view with the `string` method of the `NSString` class, you use the `RTFFromRange` method for rich text. This has the effect of retrieving the text with its style information (bold, size, color, and so on) intact:

```objective-c
[[textView RTFFromRange:
        NSMakeRange(0, [[textView string] length])]
   writeToFile: [theSavePanel filename]
   atomically: YES];
```

The only parameter of the `RTFFromRange` method is an `NSRange` value indicating the portion of text that you want to retrieve from text view. To retrieve all the text, you supply the method with the starting point of the text and the length of text to grab. In this instance, you grab all the text found in the text view, starting from position 0 (zero) and extending the length of the text in the text view:

```objective-c
NSMakeRange(0, [[textView string] length])
```

After you have `NSString` from `TextView`, `writeToFile` works the same as it does for plain text files, with a minor caveat. When you use the `writeToFile` method, the resulting plain text files have the `.txt` file extension and rich text files have the `.rtf` extension.

## Retrieving Text

Another important task that you’ll likely need to perform regularly is opening text files. To open and read a text file, your code should do the following:

- Display an `OpenPanel` so users can choose which file they want to open.
- Read the text data from the file.
- Display that data in an `NSTextView`.

To add the capability to open and view plain and rich text files, add a few items to the interface:

1. In Xcode, add the following lines of code to the `MyTextController.h` file to define these two actions:

```objective-c
- (IBAction)openRichTextFile:(id) sender;
- (IBAction)openTextFile:(id) sender;
```

2. Navigate to the `MyTextController.m` file and implement those two actions:

```objective-c
- (IBAction) openTextFile: (id) sender
{
    NSOpenPanel *theOpenPanel = [NSOpenPanel openPanel];
    if ( [theOpenPanel runModal] == NSOKButton)
    {
        NSString *theFileName = [theOpenPanel filename];
        NSString *theFileContents = [NSString stringWithContentsOfFile:theFileName];
        [textView setString:theFileContents];
    }
}

- (IBAction)openRichTextFile: (id) sender
{
    NSOpenPanel *theOpenPanel = [NSOpenPanel openPanel];
    if ( [theOpenPanel runModal] == NSOKButton)
    {
        NSString *theFileName = [theOpenPanel filename];
        NSData *theRTFData = [NSData dataWithContentsOfFile:theFileName];
        [textView replaceCharactersInRange:
              NSMakeRange(0, [textView string] length)]
              withRTF:theRTFData];
    }
}
```

3. Open the `MainMenu.xib` file in Interface Builder.

4. To the existing window object in the XIB project window, add two additional `NSButton` controls and then change their Title Attributes in the Inspector window to **Open Plain Text** and **Open Rich Text**.

Figure 11-13 shows the new buttons.

![](img/ea40cad434a338535474e82c1a6ace20_237_0.png)

5. Control-drag from each `NSButton` in the interface to the `MyText Controller` instance in `MainMenu.xib` and then when you let go of the mouse, assign the appropriate action to that button with the black connections list overlay that appears.

In contrast to the examples from earlier in this chapter in which you saved text files, opening text files requires the use of the `NSOpenPanel` class. Opening files works in much the same manner as the `NSSavePanel`. In the two methods for opening text files, you aren't setting the title displayed in the `NSOpenPanel` (with `setTitle:`) like you did for the `NSSavePanel` earlier. You certainly could, though.

Like the `NSSavePanel`, you display the `NSOpenPanel` with the `runModal` method:

```objective-c
NSOpenPanel *theOpenPanel = [NSOpenPanel openPanel];
```

If the user selects a text file and clicks OK to open it, `runModal` returns `NSOKButton`:

```objective-c
if ([theOpenPanel runModal] == NSOKButton)
```

From there, you open the text file, read its contents, and display them in an `NSTextView`. For plain text files, it's a straightforward process to read in a text file with the `stringWithContentsOfFile` method of `NSString`:

```objective-c
NSString *theFileName = [theOpenPanel filename];
NSString *theFileContents = [NSString
stringWithContentsOfFile:theFileName];
```

To display the text in an **NSTextView**, you need only one line of code:

```objective-c
[theTextView setString:theFileContents];
```

After you’re finished working with the **NSString** objects, don’t forget to dispose of them:

```objective-c
[theFileName release];
[theRTFData release];
```

Reading rich text files requires a bit of extra work, but not too much. Instead of using an **NSString** to read text from a rich text file, you must use an **NSData** object. Call the **dataWithContentsOfFile** method of the **NSData** class to load stylized text from the file into the **NSData** object:

```objective-c
NSData *theRTFData = [NSData dataWithContentsOfFile:theFileName];
```

To display it in the text view, use the **replaceCharactersInRange** method:

```objective-c
[theTextView replaceCharactersInRange:
    NSMakeRange(0, [theTextView string] length))
    withRTF:theRTFData];
```

The **replaceCharactersInRange** method takes two parameters:

- **NSRange**: The location in the **NSTextView** where you want to display the text
- **NSData**: The rich text data that you read from the file

To test your code, choose **Build -> Build and Go** in Xcode.
