+   - `(void)` indicates there’s no return value. If the method supplied a return value, this field would indicate its type in the usual C-like way.
+   - The third field is the name of the method and also defines the string used to trigger it — `setTitle:`.
+   - The colon indicates that a parameter follows the method name. In this example, the parameter is an instance of `NSString`, which is Cocoa’s strong object data type. When a parameter is a Cocoa object, it appears as a link. If you need more information about `NSString`, click on the link to view its class reference.

Putting this information together, you can guess that the message you need to send to window looks like this:

```
```objc
[window setTitle: aString];
```
```

`aString` can be defined as in-line literal using the `@` objectification character. So your final code looks like this:

```
```objc
[window setTitle: @"A Window Title"];
```
```

# Introducing Code Sense

To add this code, type it after the comment line in `applicationDidFinishLaunching:`. You’ll notice that as soon as you type the open square bracket and win, Xcode completes the rest of the window. Similarly when you type `setT`, Xcode automatically expands it to `setTitle:` and also adds a reminder field that tells you that `setTitle:` takes a parameter string.

This autocompletion feature is called Code Sense. Code Sense doesn’t read your mind — this may change in future versions of Xcode — but it does try to predict your typing and insert likely items from the application’s symbol table. The table includes the full set of Cocoa objects by default.

Code Sense can dramatically improve your productivity, but it can take a while to get used to having an assistant that makes guesses as you type:

+   - To accept a guess, press the Tab key. The cursor moves past the guess.
+   - When a symbol has multiple substring options — for example `setT` could be read as `setTitle:` or `setTitleWithRepresentedFilename:` — press the Return key to accept a part-symbol. The cursor moves to the next substring.
+   - To set a reminder field, tab to it and start typing. Your input overwrites the reminder string. For classes with multiple parameters, tab to each field in turn.