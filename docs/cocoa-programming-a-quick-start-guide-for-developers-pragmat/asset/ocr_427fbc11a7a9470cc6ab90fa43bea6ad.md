+   - Don’t choose overly complicated pages or pages that need authentication. This is a very basic web browser.
+   - Once a second page appears, you can hit the Back and Forward buttons to navigate back and forth between the two pages.

This is great! At least here in the simulator, you have a working web browser.

Our browser doesn’t have some of the features you might expect to see in even the sparsest of browsers. For example, you don’t get any feedback when a page is loading. When you first run SimpleBrowser, you might think that nothing is happening until, after a pause, the page appears. Also, the URL doesn’t change when you hit Back and Forward. If you load http://pragprog.com and then http://apple.com and then hit the Back button, you will see the Pragmatic Programmer’s home page even though the URL will still read http://apple.com. We’ll take care of these problems in the next few chapters.

# 2.6 Fixing the Build

It feels like you’re done. You can play with your application in the Cocoa Simulator. All of your work in Interface Builder is correct and complete, and you have no code to write for this SimpleBrowser project. You don’t, however, have an application that you can give to someone else to run on their machine. You need to go back to Xcode and create a release.

In Xcode, click Build & Run. The build succeeds, and it looks as if SimpleBrowser starts to load. The icon bounces in the Dock for a while, but nothing is happening. Depending on how you’re set up, you might find yourself in the debugger with a stack trace and a warning.

Arrgghhhh. Click the Stop button, or choose Run > Stop.⁸ We need to add WebKit.framework.

I mentioned earlier we’d have to link it in. We could have done it when we dragged the WebView from the Library into our window. Chances are that you’ll be more likely to remember it now that you see the problems

⁷ The point of this example is not to build a robust web browser but to use a web browser as an example application that allows us to introduce you to Cocoa programming. Currently, for example, you won't be able to load pages that include Flash.

⁸ If your installation of Xcode doesn’t look like mine, you can always customize the toolbar by choosing View > Customize Toolbar... Also, you can make many adjustments from Xcode > Preferences.