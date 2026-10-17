# RENAMING SYMBOLS

```
NSString * bob = @"Bob";
NSLog(@"My name is %@.", bob);
```

```
NSString * robert = @"Bob";
NSLog(@"My name is %@.", robert);
```

FIGURE 13.1 All instances of the symbol bob underlined

FIGURE 13.2 In the current scope, bob is now robert.

The Edit All in Scope command is a simple and often overlooked editor feature. As its name suggests, you can edit a symbol name and automatically change each instance of it within the current scope at the same time.

Consider a local variable named bob. You’ve decided a variable should sound more formal, so you want to change bob to robert. Assuming bob is reused throughout the current scope of a long method, it would be tedious and error-prone to find and rename each instance, even though they’re temporarily underlined when one instance is selected. To formalize bob, you can click the symbol, placing the insertion point somewhere inside its text. All instances of bob within the current scope then appear with a dotted underline (Figure 13.1).

If you hover your mouse pointer over any highlighted bob, you’ll notice a button appears immediately to its right. Click this button to open a context menu, and select Edit All in Scope. Xcode responds by highlighting each bob in the current scope, ready to edit them all. Begin typing to replace the text, or move the cursor around within the highlighted text to modify it. In this example, every instance of bob has been renamed to robert (Figure 13.2).

Click to place the text insertion point somewhere outside the symbol to end editing. Note that only the symbol name changed. It remains a pointer to the string literal @"Bob". You could further edit the symbol to give robert a sex change. Repeat the procedure, but instead of replacing the text, place the cursor after the t in robert and then add an a. The symbol should now be roberta, who is suddenly in need of a new wardrobe or at least a new string literal.

It’s important to note that this operation works only within the current scope. You cannot use this feature to rename an instance variable or a method.