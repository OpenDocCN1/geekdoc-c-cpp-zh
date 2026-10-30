> NOTE
> The Window group does not show on the Home tab if you're using tabbed documents (the default setting in Access 2019). To change between overlapping windows and tabbed documents, set the Document Window Options in the Current Database section of Access Options.

# Text Formatting

The Text Formatting group lets you change the look of text fields in the datasheet. Use these commands to change the font, size, bold, italic, color, and so on. Selecting a font attribute (such as bold) applies the attribute to all fields in the datasheet. (See the following Note for the only exception to this rule.) Use the Align Left, Align Right, and Center commands to align the data in the selected column. Click the Gridlines command to toggle gridlines on and off. Use the Alternate Row Color or Background Color command to change the colors of alternating rows or to make them all the same.

> NOTE
> The controls in the Text Formatting group behave differently when the currently selected field in the datasheet happens to be the Long Text data type. When a Long Text field is selected, you can change the font attributes (bold, underline, italics, and so on) of individual characters and words in the field, but only if the Text Format property is set to Rich Text. The Text Format property (which applies only to the Long Text data type) is set to Plain Text by default.

# Opening a Datasheet

Follow these steps to open a datasheet from the Database window:

+   1. Using the Chapter05.accdb database from this book's website, click Tables in the Navigation pane.
+   2. Double-click the table name you want to open (in this example, tblProducts).

An alternative method for opening the datasheet is to right-click tblProducts and select Open from the shortcut menu.

> TIP
> If you're in any of the design windows, click the Datasheet View command in the View group of the Ribbon to view your data in a datasheet.

# Entering New Data

All the records in your table are visible when you first open it in Datasheet view. If you just created your table, the new datasheet doesn't contain any data. Figure 5.4 shows an empty