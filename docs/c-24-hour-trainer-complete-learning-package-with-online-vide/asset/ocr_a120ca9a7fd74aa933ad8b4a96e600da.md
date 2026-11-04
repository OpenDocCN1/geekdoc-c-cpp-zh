Font
Small	Ctrl+S
Normal	Ctrl+N
Large	Ctrl+L

+   - Add code behind the main menu items.
+   - Make the context menu duplicate the main menu's Format submenu.
+   - Attach the context menu items to the same event handlers used by the main menu.
+   - Attach the context menu to the TextBox.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

# Hints

+   - The Exit menu item can close the program's form by calling this.Close().
+   - Creating a font isn't trivial (and I haven't covered that yet). It's much easier to keep a sample of a font in a control somewhere on the form and then set the TextBox's Font property equal to that control's Font property. And what better control to store the font than the menu item itself?

# Step-by-Step

+   - Create the form shown in Figure 5-8.
+     1. Create the main menu by double-clicking the Toolbox's MenuStrip tool.
+     2. Add a TextBox to the form. Type some text into its Text property and set its properties: Name = contentsTextBox, Multiline = True, Dock = Fill, ScrollBars = Both.
+     3. Create the context menu by double-clicking the Toolbox's ContextMenuStrip tool.

+   - Create the main menu structure.
+     1. Select the MenuStrip. Click the Type Here box and type &File.
+     2. In the Type Here box below the File menu, type E&xit.

> NOTE By convention, the Exit command uses X as its accelerator. It never has a shortcut because it would be too easy to accidentally close the program while banging your head on the keyboard (or if you fat-finger the keys, the keyboard is hit by a flying tennis ball, or your cat walks across the keyboard).