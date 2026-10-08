# *Connecting the actions to the interface*

Incidentally, you don’t have to create actions in Interface Builder. Actions are just as valid if you declare them in Xcode. You still have to connect actions to their desired interface elements in Interface Builder, though, so do that now:

+   1.  **Double-click the MainMenu.xib file in the Resources group of your project in Xcode** to return to Interface Builder.
2.  **In the XIB project window of Interface Builder, select** *MyAudioController*.
3.  **Choose File** **Read Class Files** and select *MyAudioController.h* at the prompt.

Interface Builder checks the header files for any changes. Because you added a new stopSoundFile action in Xcode, Interface Builder updates the MainMenu.xib NIB file, adding the new action as shown in Figure 16-5.

+   4.  **Add a new button to the main window of your interface by dragging** one from the Library window and labeling it *Stop Sound File*.

Figure 16-6 shows the result.

![](bbox=[0.24, 0.5, 0.77, 0.86])

**Figure 16-5:** If you add actions or outlets in Xcode, Interface Builder can find them in the header files and update the NIB file accordingly.