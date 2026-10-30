
# Moving among records in a form

Although you generally use a form to display one record at a time, you still need to move between records. The easiest way to do this is to use the Navigation buttons, shown in Figure 18.3.

The Navigation buttons are the six controls located at the bottom-left corner of the Form window. The two leftmost controls move you to the first record and the previous record in the form. The three rightmost controls position you on the next record, last record, or new record in the form. If you know the record number (the row number of a specific record), you can click the Current Record box, enter a record number, and press Enter to go directly to that record.

## FIGURE 18.3

The Navigation buttons of a form.

![](img/1e45673ab6eca9d20e67635ff5b9b318_580_0.png)

The record number displayed in the Navigation controls is just an indicator of the current record's position in the recordset and may change when you filter or sort the records. To the right of the record number is the total number of records in the current view. The record count may not be the same as the number of records in the underlying table or query. The record count changes when you filter the data on the form.

## Changing Values in a Form

Earlier in this book, you learned datasheet techniques to add, change, and delete data within a table. These techniques are the same ones you use on an Access form. Table 18.2 summarizes these techniques.

## TABLE 18.2 Editing Techniques

| Editing Technique | Keystrokes |
|---|---|
| Move insertion point within a control | Press the right-arrow (→) and left-arrow (←) keys |
| Insert a value within a control | Position the insertion point and type new data |
| Select the entire contents of a control | Press F2 |
| Replace an existing value with a new value | Select the entire field and enter a new value |
| Replace a value with the value of the preceding field | Press Ctrl+' (single quotation mark) |
| Replace the current value with the default value | Press Ctrl+Alt+Spacebar |

Continues

## Part V: Working with Access Forms and Reports

## TABLE 18.2 (continued)

| Editing Technique | Keystrokes |
|---|---|
| Insert the current date into a control | Press Ctrl+; (semicolon) |
| Insert the current time into a control | Press Ctrl+: (colon) |
| Insert a line break in a Text control | Press Ctrl+Enter |
| Insert a new record | Press Ctrl++ (plus sign) |
| Delete the current record | Press Ctrl+– (minus sign) |
| Save the current record | Press Shift+Enter or move to another record |
| Toggle values in a check box or option button | Spacebar |
| Undo a change to the current control | Press Esc or click the Undo button |
| Undo a change to the current record | Press Esc or click the Undo button a second time after you Undo the current control |

> NOTE
> The right-arrow (->) and left-arrow (<-) keys work differently in Navigation mode than they do in Edit mode. The F2 key switches between Navigation mode and Edit mode. The only visual cue for the mode that you're in is that the insertion point is displayed in Edit mode. The arrow keys navigate between controls in Navigation mode and are used to select text in Edit mode.

## Knowing which controls you can't edit

Some controls, including the following, can't be edited:

- Controls displaying AutoNumber fields: Access maintains AutoNumber fields automatically, calculating the values as you create each new record.
- Calculated controls: Access may use calculated controls in forms or queries. Calculated values are not actually stored in your table.
- Locked or disabled fields: You can set certain form and control properties to prevent changes to the data.
- Controls in multiuser locked records: If another user locks the record, you can't edit any controls in that record.

## Working with pictures and OLE objects

Object Linking and Embedding (OLE) objects are objects not part of an Access database. OLE objects commonly include pictures but may be any number of other data types, such as links to Word documents, Excel spreadsheets, and audio files. You can also include video files such as MPG or AVI files.

In Datasheet view, you can’t view a picture or an OLE object without accessing the OLE server (such as Word, Excel, or the Windows Media Player). In Design view, however, you can size the OLE control area to be large enough to display a picture, chart, or other OLE objects in Form view. You can also size Text Box controls on forms so that you can see the data within the field—you don’t have to zoom in on the value, as you do with a datasheet field.

The Access OLE control supports many types of objects. As with a datasheet, you have two ways to enter OLE fields into a form:

- Copy the object (such as an MP3 file) to the Clipboard and paste it from the controls in the Clipboard group of the Ribbon.
- Right-click the OLE control and click Insert Object from the shortcut menu to display the Insert Object dialog box, shown in Figure 18.4. Use the Insert Object dialog box to add a new object to the OLE field, or add an object from an existing file. The Create from File option button adds a picture or other OLE object from an existing file.

## FIGURE 18.4
The Insert Object dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_582_0.png)

When displaying a picture in an OLE control, set the Size Mode property to control how the image representing the OLE object is displayed. The settings for this property are:

- Clip: Keeps the image at its original size and cuts off parts of the picture that don’t fit in the control.
- Zoom: Fits the image in the control and keeps it in its original proportion, which may result in extra white space.
- Stretch: Sizes an image to fit exactly between the frame borders. The stretch setting may distort the picture.

## Entering data in the Long Text field

The Features field in the frmProducts form is a Long Text data type. This type of field contains up to 1GB of characters. The first four lines of data appear in the text box. When you click in this text box, a vertical scroll bar appears, allowing you to view all the data in the control.

Better yet, you can resize the control in the form's Design view if you want to make it larger to show more data. Another method for viewing more text in a Long Text field's text box is to press Shift+F2 with the text box selected. A Zoom dialog box is displayed, as shown in Figure 18.5, allowing you to see more data. The text in the Zoom dialog box is fully editable. You can add new text or change text already in the control.

## FIGURE 18.5

The Zoom dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_583_0.png)

## Entering data in the Date field

The SaleDate field in the frmSales_Layout form is a Date/Time data type. This field is formatted to accept and show date values. When you click in this text box, a Date Picker icon

automatically appears next to it, as shown in Figure 18.6. Click the Date Picker to display a calendar from which you can choose a date.

## FIGURE 18.6

Using the Date Picker control.

![](img/1e45673ab6eca9d20e67635ff5b9b318_584_0.png)

If the Date Picker doesn’t appear, switch to Design view and change the control’s Show Date Picker property to For Dates. Set the Show Date Picker property to Never, as shown in Figure 18.7, if you don’t want to use the Date Picker.

## FIGURE 18.7

Change the Show Date Picker property to Never to disable it.

![](img/1e45673ab6eca9d20e67635ff5b9b318_584_1.png)

## Using option groups

Option groups let you choose exactly one value from a number of possibilities. Option groups work best when you have a small number of mutually exclusive choices to select from. Figure 18.8 shows an option group next to the Follow-Up Date text box. Option groups most commonly contain option buttons but also work with toggle buttons and check boxes.

## FIGURE 18.8

Using an option group to select a mutually exclusive value.

![](img/1e45673ab6eca9d20e67635ff5b9b318_585_0.png)

The easiest and most efficient way to create option groups is with the Option Group Wizard. You can use it to create option groups with multiple option buttons, toggle buttons, or check boxes. When you're through, all your control's property settings are correctly set. To create an option group, switch to Design view and select the Option Group button from the Design tab's Controls group. Make sure the Use Control Wizards command is selected in the Controls group.

Each element in an option group is assigned a number in its Option Value property. When an option group is bound to a field, the Option Value is stored in that field when the record is saved.

Tip
When creating an option group for a Yes/No field (which is actually stored as a number), set the Yes value to -1 and the No value to 0.

## Using combo boxes and list boxes

Access has two types of controls—list boxes and combo boxes—for showing lists of data from which a user can select. The list box always displays as much of the list as possible, whereas the combo box has to be clicked to open the list. A combo box is a combination of a text box and a list box. The text box portion of a combo box is always visible, and the user can enter text into it just like any other text box. The user can also click the drop-down arrow to display the list box portion of the combo box and select an item rather than typing it.
