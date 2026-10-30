
> NOTE
> The Window group does not show on the Home tab if you're using tabbed documents (the default setting in Access 2019). To change between overlapping windows and tabbed documents, set the Document Window Options in the Current Database section of Access Options.

## Text Formatting

The Text Formatting group lets you change the look of text fields in the datasheet. Use these commands to change the font, size, bold, italic, color, and so on. Selecting a font attribute (such as bold) applies the attribute to all fields in the datasheet. (See the following Note for the only exception to this rule.) Use the Align Left, Align Right, and Center commands to align the data in the selected column. Click the Gridlines command to toggle gridlines on and off. Use the Alternate Row Color or Background Color command to change the colors of alternating rows or to make them all the same.

> NOTE
> The controls in the Text Formatting group behave differently when the currently selected field in the datasheet happens to be the Long Text data type. When a Long Text field is selected, you can change the font attributes (bold, underline, italics, and so on) of individual characters and words in the field, but only if the Text Format property is set to Rich Text. The Text Format property (which applies only to the Long Text data type) is set to Plain Text by default.

## Opening a Datasheet

Follow these steps to open a datasheet from the Database window:

- 1. Using the Chapter05.accdb database from this book's website, click Tables in the Navigation pane.
- 2. Double-click the table name you want to open (in this example, tblProducts).

An alternative method for opening the datasheet is to right-click tblProducts and select Open from the shortcut menu.

> TIP
> If you're in any of the design windows, click the Datasheet View command in the View group of the Ribbon to view your data in a datasheet.

## Entering New Data

All the records in your table are visible when you first open it in Datasheet view. If you just created your table, the new datasheet doesn't contain any data. Figure 5.4 shows an empty datasheet and a portion of the Fields tab of the Ribbon. When the datasheet is empty, the first row contains an asterisk (*) in the record selector, indicating it's a new record.

### FIGURE 5.4

An empty datasheet. Notice that the first record is blank and has an asterisk in the record selector.

![](img/1e45673ab6eca9d20e67635ff5b9b318_179_0.png)

The Table Tools tab group of the Ribbon includes virtually all the tools needed to build a complete table. You can specify the data type, default formatting, indexing, field and table validation, and other table construction tasks from the controls in the Table Tools tab group.

The New row appears at the bottom of the datasheet when the datasheet already contains records. Click the New command in the Records group of the Ribbon, or click the New Record button in the group of Navigation buttons at the bottom of the datasheet to move the cursor to the New row—or simply click the last row, which contains the asterisk. The asterisk turns into a pencil when you begin entering data, indicating that the record is being edited. A new row—containing an asterisk—appears below the one you're entering data into. The new record pointer always appears in the last row of the datasheet. Figure 5.5 shows adding a new record to tblProducts.

### FIGURE 5.5

Entering a new record into the Datasheet view of tblProducts.

![](img/1e45673ab6eca9d20e67635ff5b9b318_180_0.png)

Edit indicator

New row

Edited cell

To add a new record to the open Datasheet view of tblProducts, follow these steps:

- 1. Click the New button in the Records group of the Home tab of the Ribbon.
- 2. Type in values for all fields of the table, moving between fields by pressing the Enter key or the Tab key.

When adding or editing records, you might see three different record pointers:

- Record being edited: A pencil icon
- Record is locked (multiuser systems): A padlock icon
- New record: An asterisk icon

## CAUTION

If the record contains an AutoNumber field, Access shows the name (New) in the field. You can't enter a value in this type of field; instead, simply press the Tab or Enter key to skip the field. Access automatically puts the number in when you begin entering data.

## Saving the record

Moving to a different record saves the record you're editing. Tabbing through all the fields, clicking the Navigation buttons, clicking Save in the Records group of the Ribbon, and closing the table all write the edited record to the database. You'll know the record is saved when the pencil disappears from the record selector.

To save a record, you must enter valid values into each field. The fields are validated for data type, uniqueness (if indexed for unique values), and any validation rules that you've entered into the Validation Rule property. If your table has a primary key that's not an AutoNumber field, you'll have to make sure you enter a unique value in the primary key field to avoid the error message shown in Figure 5.6. One way to avoid this error message while entering data is to use an AutoNumber field as the table's primary key.

### FIGURE 5.6

The error message Access displays when attempting to save a record with a duplicate primary key value entered into the new record. Use an AutoNumber field as your primary key to avoid this error.

![](img/1e45673ab6eca9d20e67635ff5b9b318_181_0.png)

### Tip

The Undo button in the Quick Access toolbar reverses changes to the current record and to the last saved record. After you change a second record, you can't undo a previously saved record.

### Tip

You can save the record to disk without leaving the record by pressing Shift+Enter.

Now you know how to enter, edit, and save data in a new or existing record. In the next section, you learn how Access validates your data as you make entries into the fields.

## Understanding automatic data-type validation

Access validates certain types of data automatically. Therefore, you don't have to enter any data validation rules for these data types when you specify table properties. The data types that Access automatically validates include:

- Number/Currency
- Date/Time
- Yes/No

Access validates the data type when you move off the field. When you enter a letter into a Number or Currency field, you don’t initially see a warning that the characters are invalid. When you tab out of the field or click a different field, you get a warning like the one shown in Figure 5.7. This particular warning lets you choose to enter a new value or change the column’s data type to Text. You’ll see this message if you enter other invalid characters (symbols, letters, and so on), enter more than one decimal point, or enter a number too large for the specified numeric data type.

### FIGURE 5.7

The warning Access displays when entering data that doesn’t match the field’s data type. Access gives you a few choices to correct the problem.

![](img/1e45673ab6eca9d20e67635ff5b9b318_182_0.png)

Access validates Date/Time fields for valid date or time values. You’ll see a warning similar to the one shown in Figure 5.7 if you try to enter a date such as 14/45/05, a time such as 37:39:12, or an invalid character in a Date/Time field.

Yes/No fields require that you enter one of these defined values:

- **Yes:** Yes, True, On, -1, or a number other than 0 (which displays as -1)
- **No:** No, False, Off, or 0

## Part II: Understanding Access Tables

Of course, you can define your own acceptable values in the Format property for the field, but generally these values are the only acceptable ones. If you enter an invalid value, the warning appears with the message to indicate an inappropriate value.

> **TIP**
> 
> The default value of a Yes/No field’s Display Control is Check Box. Displaying a check box in Yes/No fields prevents users from entering invalid data.

## Knowing how properties affect data entry

Because field types vary, you use different data-entry techniques for each type. In the “Saving the record” section earlier in this chapter, you learned that some data-type validation is automatic. Designing tblContacts, however, means entering certain user-defined format and data validation rules. The following sections examine the types of data entry.

## Standard text data entry

The first field—ContactID—in tblContacts is an AutoNumber field, while other fields in the table are Short Text fields. After skipping ContactID, you simply enter a value in each field and move on. The zipcode field uses an input mask (00000)–9999;–) for data entry. The Phone and Fax fields also use an input mask (\(999\) "000\-0000;_). A 0 in an input mask represents a required numeric entry. A 9 in an input mask represents an optional numeric entry. The zipcode input mask requires the first five digits, but the plus 4 portion is optional. Short Text fields accept any characters, unless you restrict them with an input mask.

> **TIP**
> 
> To enter multiple lines in a Short Text or Long Text field, press Ctrl+Enter to add a new line. This is useful, for example, in large text strings for formatting a multiple-line address field.

## Date/Time data entry

The OrigCustDate and LastSalesDate fields in tblContacts are Date/Time data types, which both use a Short Date format (3/16/2019). However, you could have defined the format as Medium Date (16-Mar-19) or Long Date (Saturday, March 16, 2019). Using either of these formats simply means that no matter how you type in the date—using month and year; day, month, and year; or month, day, and year—the date always displays in the specified format (short date [3/16/2019], medium date [16-Mar-19], or long date [Saturday, March 16, 2019]). Therefore, if you type 3/16/19 or 16 Mar 19, Access displays the value in the specified format as you leave the field. Dates are actually stored in the database without any formatting, so the format you select for a field doesn’t affect how the data is stored.
