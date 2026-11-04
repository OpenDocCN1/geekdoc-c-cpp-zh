
Gestures are quite powerful, but they're also fairly complicated so I'm not going to cover them in this book. You can learn more about them in the article “Commanding Overview” at msdn.microsoft.com/en-us/library/ms752308. Meanwhile, you can just create click event handlers for menu items.

## TRY IT

In this Try It, you create a main menu and a context menu. The main menu includes an Exit command that closes the form. Both menus contain commands that let you change the appearance of a TextBox on the form. Figure 5-8 shows the finished program displaying its context menu.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_119_0.png)

FIGURE 5-8

## Lesson Requirements

In this lesson, you:

- Create the form shown in Figure 5-8.
- Create the following main menu structure (note the accelerator keys and shortcuts):
  File
    Exit
  Format
    Color
      Red Ctrl+R
      Green Ctrl+G
      Blue Ctrl+B
    Background Color
      Pink
      Light Green
      Light Blue
  Font
    Small Ctrl+S
    Normal Ctrl+N
    Large Ctrl+L
- Add code behind the main menu items.
- Make the context menu duplicate the main menu's Format submenu.
- Attach the context menu items to the same event handlers used by the main menu.
- Attach the context menu to the TextBox.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

## Hints

- The Exit menu item can close the program's form by calling this.Close().
- Creating a font isn't trivial (and I haven't covered that yet). It's much easier to keep a sample of a font in a control somewhere on the form and then set the TextBox's Font property equal to that control's Font property. And what better control to store the font than the menu item itself?

## Step-by-Step

- Create the form shown in Figure 5-8.
  1. Create the main menu by double-clicking the Toolbox's MenuStrip tool.
  2. Add a TextBox to the form. Type some text into its Text property and set its properties: Name = contentsTextBox, Multiline = True, Dock = Fill, ScrollBars = Both.
  3. Create the context menu by double-clicking the Toolbox's ContextMenuStrip tool.

- Create the main menu structure.
  1. Select the MenuStrip. Click the Type Here box and type &File.
  2. In the Type Here box below the File menu, type E&xit.

> NOTE By convention, the Exit command uses X as its accelerator. It never has a shortcut because it would be too easy to accidentally close the program while banging your head on the keyboard (or if you fat-finger the keys, the keyboard is hit by a flying tennis ball, or your cat walks across the keyboard).

  3. Click the File item again. In the Type Here box to the right, type F&ormat. (You can't use the F character as this menu's accelerator because it's already used by the File menu.)
  4. Use the Type Here boxes below the Format menu to create the format menu items and their submenus.
  5. Use the Properties window to set the font sizes for the Font menu's Small, Normal, and Large items to 6, 9, and 20, respectively.
  6. Give the Color and Font submenu items appropriate shortcuts.
  7. Give the menu items that take action appropriate names. For example, name the Font menu's Small item formatFontSmallMenuItem.

### Add code behind the main menu items.

  1. Double-click the Exit menu item and type the bold line in the following code so the event handler looks like this:

```
private void fileExitMenuItem_Click(object sender, EventArgs e)
{
    this.Close();
}
```

The keyword this means "the object currently executing this code," which in this case means the current form, so this line of code tells the current form to close itself.

  2. Double-click the Format ▸ Color ▸ Red menu item and type the bold line in the following code so the event handler looks like this:

```
private void formatColorRedMenuItem_Click(object sender, EventArgs e)
{
    contentsTextBox.ForeColor = Color.Red;
}
```

  3. Repeat step 2 for the Green and Blue menu items.
  4. Repeat step 2 for the Format ▸ Background Color menu items.

  5. Double-click the Format ▸ Font ▸ Small menu item and type the bold line in the following code so the event handler looks like this:

```
private void formatFontSmallMenuItem_Click(object sender, EventArgs e)
{
    contentsTextBox.Font = formatFontSmallMenuItem.Font;
}
```

- Copy the Format menu's structure. (This is sneakier and faster, and therefore much cooler!)
  a. Click the MenuStrip in the Component Tray to open it for editing. Expand the Format menu. Click the Color item and then shift-click the Font item to select all of the menu's items. Press Ctrl+C to copy the menu items into the clipboard.
  b. Click the ContextMenuStrip in the Component Tray to open it for editing. Press Ctrl+V to paste the menu items into the context menu.
  c. Give appropriate names to the new menu items.

- Attach the context menu items to the event handlers used by the main menu.
  1. Open the ContextMenuStrip for editing. Expand the Color submenu and click the Red item. In the events page of the Properties window, select the Click event. Open the dropdown on the right and select formatColorRedMenuItem_Click.
  2. Repeat step 1 for the ContextMenuStrip's other items, attaching them to the correct event handlers.

- Attach the context menu to the TextBox.
  1. Click the TextBox. In the Properties window, set its ContextMenuStrip property to formatContextMenu.

## EXERCISES

  1. [WPF] Repeat the Try It with a WPF application Hints:
     - You might save time by building some menus and then copying and pasting them in the XAML Code Editor.
     - Set the TextBox's colors as in `contentsTextBox.Foreground = Brushes.Red`.
     - Set the TextBox's font size as in `contentsTextBox.FontSize = formatFontSmallMenuItem.FontSize`.

  2. [SimpleEdit] Copy the SimpleEdit program you started in Lesson 3, Exercise 4 (or download Lesson 3's version from the book's website at www.wrox.com) and add the following menu structure. Set the Checked property of the bold items to True.

    File
    - New    Ctrl+N
    - Open...    Ctrl+O
    - Save    Ctrl+S
    - Save As...
    - -
    - Print Preview...
    - Print...    Ctrl+P
    - -
  - Exit
  - Edit
    - Undo Ctrl+Z
    - Redo Ctrl+Y
    - -
    - Copy Ctrl+C
    - Cut Ctrl+X
    - Paste Ctrl+V
    - Delete Del
    - -
    - Select All Ctrl+A
  - Format
    - Align
      - Left
      - Right
      - Center
    - Text Color...
    - Background Color...
    - Bullet
    - Offset
      - Normal
      - Subscript
      - Superscript
    - Font...
    - Indent
      - None
      - Hanging
      - Left
      - Right
      - Both

Add the code behind the Exit item, but don't worry about the other items yet.

Eventually the user will be able to use the Bullet menu item to toggle whether a piece of text is bulleted. To allow C# to toggle this item for you, set the menu item's CheckOnClick property to True.

Add a ContextMenuStrip that duplicates the Format menu and use it for the TextBox's ContextMenuStrip property.

  3. [WPF, SimpleEdit] Repeat Exercise 2 with a WPF application. Hint: To check a menu item, set its IsChecked property to True.

  4. [SimpleEdit] Copy the SimpleEdit program you built for Exercise 1 and add images to its menu and context menu items. (You can find suitable image files in the PngFiles directory of the Lesson 5 downloads available on the book's website.) Figure 5-9 shows what the menus should look like when you're finished.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_124_0.png)

FIGURE 5-9

  5. [WPF, SimpleEdit] Repeat Exercise 4 with the WPF application you built for Exercise 3. The Properties window in the version of Visual Studio I'm using doesn't seem to allow you to set a menu item's Icon property, but this isn't too hard to do in the XAML editor. First use the Project menu's Add Existing Item command to add the image files to the project. Then use XAML code similar to the following to add icons to the appropriate menu items:

```
<MenuItem Header="New" Name="fileNewMenuItem">
    <MenuItem.Icon>
        <Image Source="New.png" />
    </MenuItem.Icon>
</MenuItem>
```

  6. [SimpleEdit] Copy the SimpleEdit program you built for Exercise 4 and add placeholder routines for the menu items' event handlers. The routines should display simple message
