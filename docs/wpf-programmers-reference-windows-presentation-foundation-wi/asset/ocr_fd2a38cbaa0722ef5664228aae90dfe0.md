# RichTextBox | 137

| COMMAND NAME | SHORTCUT |
|---|---|
| ToggleNumbering | [Ctrl]+[Shift]+N |
| ToggleScript | [Ctrl]+OemPlus |
| ToggleSuperscript | [Ctrl]+[Shift]+OemPlus |
| ToggleUnderline | [Ctrl]+U |

The OpenBracket, CloseBracket, and OemPlus keys are the OEM (Original Equipment Manufacturer) [], and characters. These are usually placed in the keypad area, and depending on your keyboard hardware, similar keys in other parts of the keyboard may not work. For example, the + key in the keypad area might work but the + key to the number keys may not.

For more information about editing commands and a more complete list, see msdn.microsoft.com/system.windows.documents.editingcommands.aspx.

# # Spell Checking

One of the RichTextBox control's most exciting features is support for spell checking. If you set the control's SpellCheck.IsEnabled property to True, then the control automatically highlights likely errors.

By default, the RichTextBox control provides a context menu containing the Copy, Cut, and Paste. If spell checking is enabled and you left-click over a misspelled word, then the context menu also includes a list of possible corrections and an "Ignore All" command. If you select one of the suggestions, the control replaces the misspelled version with your selection. If you select "Ignore All", the control treats all occurrences of the misspelled word as correctly spelled.

Figure 7-14 shows the UseRichTextBox program displaying its context menu.

![](bbox=[0.613, 0.535, 0.932, 0.695])

FIGURE 7-14

# # Undo and Redo

The RichTextBox control automatically provides undo and redo features. Each time the user presses [Ctrl]+Z, the control undoes the most recent change. Each time the user presses [Ctrl]+Y, the control reapplies the most recently undone change.

The control also provides tools that you can use to manage the undo stack programmatically. CanUndo and CanRedo properties indicate whether there is an action that the control can undo or redo. The Undo and Redo methods call the undo or redo an action.

The RichTextBox program's Edit menu contains Undo and Redo commands. When the user opens the Edit menu, the following code checks the RichTextBox control's CanUndo and CanRedo properties