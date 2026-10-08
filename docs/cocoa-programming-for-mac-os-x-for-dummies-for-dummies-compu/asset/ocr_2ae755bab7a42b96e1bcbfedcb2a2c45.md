```
- (void)awakeFromNib {
	[theWindow makeKeyAndOrderFront:nil];
	[theMenuWindow makeKeyAndOrderFront:nil];
}

@end
```

8. **Choose Build** **⌘B** and Go to test the project.

# # Changing the Appearance of Windows

Beauty may be only skin deep, but when it comes to using your application, an attractive interface is mandatory. In this section, you explore some of the possible window settings for nice-looking interfaces. These features also enhance the functionality of your applications, so you have some brawn to go with that beauty.

# ## Using different windows 
## for different tasks

The standard Mac window style has a gray background, as shown in Figure 8-2. However, this isn’t the only appearance a window can have. Apple has strict guidelines about how windows should look, which are outlined in the famous Human Interface Guidelines document available online at developer.apple.com. The basic gist of the Apple guidelines is that windows should look the same for the same tasks. A document window looks one way. A toolbar window looks a different way. A window in a one-window application should look yet another way. Always follow Apple’s guidelines when designing interface windows because your users expect windows to look and behave identically across applications.

Open the default XIB file from a Cocoa application in Interface Builder. You can change the appearance of a window by following these steps:

+   1.  **Open the default window in Interface Builder.**
Double-click it in the XIB project window.
2.  **Press ⌘+1 to open the Inspector window.**
In the Attributes section of the Inspector window, you find the Textured check box for the window.