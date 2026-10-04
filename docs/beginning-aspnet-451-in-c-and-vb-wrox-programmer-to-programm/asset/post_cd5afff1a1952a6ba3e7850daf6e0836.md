
# The Find Results Window

The Find and Replace features of VS are invaluable tools when it comes to managing the content of your site. You will often need to replace some text in the current document or even in the entire site. Find in Files (Ctrl+Shift+F) and Replace in Files (Ctrl+Shift+H) both output their results in the Find Results window, as shown in Figure 1-13.

![](img/9e033e3b9560597824f8b22941d6d8bb_60_0.png)

Figure 1-13

Because having several informational windows open at the same time may take up precious screen space, it's often a good idea to dock them. This way, only one of them is visible at a time, while you still have quick access to the others. You learn how to customize the IDE, including the docking of windows, next.

# CUSTOMIZING THE IDE

Although the standard setup of Visual Studio and its tool windows is pretty useful, there's a fair chance you want to customize the IDE to your liking. You may want to move some of the windows to a location where they are easier to reach, or you may want to open additional windows you frequently use. Visual Studio is fully customizable and enables you to tweak every little detail of the IDE. In the next section, you learn how to perform the most common customization tasks.

# Rearranging Windows

To give each window the location it deserves, you can drag and drop them in the main IDE. Simply grab a window's title bar or drag it in the direction of the new location. Once you start dragging, you see that Visual Studio gives you cues as to where the window will end (see Figure 1-14).

If you drag over one of the four square indicators at the sides of the middle indicator, the window will be docked next to the existing window. Once you drop it, the window pops to its new location. If you drop it on the square in the middle of the large indicator, the window docks with that window, sharing the same screen space. Each window has its own tab, as you can see with windows at the bottom of Figure 1-14.

In addition to docking windows with others in the IDE, you can also have floating windows. To change a docked window into a floating one, drag it away from its current location and drop it somewhere in the IDE without hitting one of the visual cues on the screen. You can also choose Window -> Float from the main menu or right-click the window's title bar and choose Float.

# CHAPTER 1 GETTING STARTED WITH ASP.NET 4.5.1

![](img/9e033e3b9560597824f8b22941d6d8bb_61_0.png)

FIGURE 1-14

To restore a floating panel to its previous docked location, right-click its title bar and choose Dock or choose Window ⬍ Dock from the menu. Make sure you don't choose Dock as Tabbed Document for the tool windows, like the Toolbox or the Solution Explorer, and they'll end up in the main Document window. This makes it difficult to use these tools together with an open file because the two windows share the same space.

# Modifying the Toolbox

You can modify the Toolbox as well. By default, the items are sorted alphabetically, but you can reorder them using drag and drop. To do this, open the Toolbox (press Ctrl+Alt+X) drag an item (such as the TextBox under the Standard category) to a different location. You can also delete items from the Toolbox by right-clicking them and choosing Deleting from the context menu. Or by avoiding items getting lost for free; you can restore the Toolbox by choosing Reset Toolbox from the same menu.

You can also add your own items to the Toolbox. The most common use for this is code snippets. Simply highlight some text or code in the Document window and drag it to the Toolbox. You can then right-click the item and choose Rename to item to give it a more meaningful name that you can easily recognize.

To avoid cluttering the Toolbox with your own code snippets, consider creating a separate category for them. You can do this by adding Add Tab from the Toolbox's right-click menu. Enter a name and press Enter, and your Toolbox tab is ready for use.

Customizing the IDE

In the next Try It exercise you get the chance to play around with the Visual Studio IDE so you can customize it to your liking.

# TRY IT OUT Customizing the IDE

In this exercise you practice opening and rearranging the windows in the VS IDE. Don't be afraid to mess things up. A little later in this chapter, instructions are given on how to reset the IDE to the way it was when you opened the first time.

- 1. If you closed your website since the previous Try It Out, open it again, or create a new one using the Menu file.
- 2. From the View menu, choose Error List to open the Error List window. If you don't see the Error List item directly, choose Tools 🛠 Settings ⚙️ Expert Settings first. Notice how the Error List gets docked below the Document window by default.
- 3. From the same view, choose Task List. By default, it is docked in the same space as the Error List, with tabs for both next to each other.
- 4. Click the tab of the Task List, and while holding your mouse button, drag the Task List away from its location in the direction of the Document Window. Once you release the window, it appears as a floating window in the IDE. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 5. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 6. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 7. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 8. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 9. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 10. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.
- 11. To restore window, drag it back to the center square of the Error List. To change the order, drag it back to the center square of the Error List.

# How It Works

Most of the steps in this Try Out are self-explanatory. By opening a few windows that you need when building websites. You used the drag-and-drop features of the IDE to rearrange the window layout according to your preferences.

You then added an HTML fragment to a control in the Toolbox. When you drag any markup to the Toolbox, Visual Studio creates a Toolbox item for it that contains the selected markup. Whenever you need a copy of that markup in your page, simply double-click the item or drag it from the Toolbox into Markup View. This is great time saver for HTML fragments that you frequently use. You typically use this technique for larger blocks of code; elements like the heading, Visual Studio has a better tool called Snippets, which you will learn about later in this book.

At the end you used Visual Studio's document formatting option to change the layout of the code in the document. This helps to keep the code organized and easy to read. You can fully change how the code is formatted using the Options dialog accessible through Tools → Options. Expand the path Text Editor -> HTML (Web Forms) → Formatting, and click Tag Options.

# Customizing the Document Window

Visual Studio gives you great flexibility with regard to how text is displayed in the Document Window. You can change things like font size, font color, and even the background color of the text. You can access the Font and Colors settings by choosing Tools → Options, and then choosing Environment. Alternatively, press Ctrl+Q to get the focus on the Quick Launch textbox at the very top of the IDE. Then type font and press Enter to select the highlighted item.
