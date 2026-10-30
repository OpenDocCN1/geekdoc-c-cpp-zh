
## Part V: Working with Access Forms and Reports

### FIGURE 21.28

txtPageNumber jumps from right to left.

![](img/1e45673ab6eca9d20e67635ff5b9b318_729_0.png)

### Using different formats in the same text box

On some reports, you may want the format of certain fields in a record to change according to the values in other fields on the report. A good example is a journal voucher report in a multicurrency financial system in which the voucher detail debit or credit amount format varies according to the number of decimal places used to display the currency value.

Unfortunately, a control in a Detail section of a report can have only one format specified in its Property Sheet. Use the following trick to set the format property at run time. The FlexFormat() function, which is stored in the MFunctions module and used in rptFlexFormat, uses the lDecimals argument to return a string specifying the desired format:

```
Public Function FlexFormat(lDecimals As Long) As String

    FlexFormat = "#,##0." & String(lDecimals, "0")

End Function
```

The String function returns text that has lDecimal number of characters and all the characters are 0. If lDecimals is 2, for example, FlexFormat returns "#,##0.00".

Assume that the field to be dynamically formatted has its Control Source set to [Amount]. The format of the Amount text box should vary depending on the value of the CurrDecPlaces field in the same record. CurrDecPlaces is a Long Integer data type. To use FlexFormat, change the Control Source property of the Amount text box to the following:

```
=Format([Amount], FlexFormat([CurrDecPlaces]))
```

The Amount text box will be dynamically formatted according to the value contained in the CurrDecPlaces text box. This trick may be generalized to format fields other than currency fields. By increasing the number of parameters of the user-defined formatting function, the formatting can be dependent on more than one field, if necessary.

### Centering the title

Centering a report title directly in the middle of the page is often difficult. The easiest way to guarantee that the title is centered is to stretch the title from left margin to right margin, and then click the Center button in the Text Formatting group of the Home tab.

### Aligning control labels

Keeping text boxes and their labels properly aligned on reports is sometimes difficult. Because a text box and its label can be independently moved on the report, all too often the label's position must be adjusted to bring it into alignment with the text box.

You can eliminate text box labels completely by including the label text as part of the text box's record source. Use the concatenation character to add the label text to the text box's control source:

```
= "Product: " & [ProductName]
```

Now, whenever you move the text box, both the label and the bound record source move as a unit. The only drawback to this technique is that you must use the same format for the text box and its label.

### Micro-adjusting controls

The easiest way to adjust the size or position of controls on a report in tiny increments is to hold down either the Shift or Ctrl key and press the arrow key corresponding to Table 21.2.

### TABLE 21.2 Micro-Adjustment Keystroke Combinations

| Key Combination | Adjustment |
|---|---|
| Ctrl+Left Arrow | Move left |
| Ctrl+Right Arrow | Move right |
| Ctrl+Up Arrow | Move up |
| Ctrl+Down Arrow | Move down |
| Shift+Left Arrow | Reduce width |
| Shift+Right Arrow | Increase width |
| Shift+Up Arrow | Reduce height |
| Shift+Down Arrow | Increase height |

Another resizing technique is to position the cursor over any of the sizing handles on a selected control and double-click. The control automatically "sizes to fit" the text contained within the control. This quick method can also be used to align not only labels but also text boxes to the grid.

### Adding Data

When you're looking at data through forms, you can usually assume that the data is current. However, with printed reports, you don't always know how old the data is. Adding little touches like when the report was printed can help increase the confidence the user has in the report. This section shows you some techniques that enable you to add additional information to the report to let the users know something of its origin.

### Adding more information to a report

You probably know that the following expression in an unbound text box prints the current page and the number of pages contained in the report:

```
="Page " & [Page] & " of " & [Pages]
```

Both Page and Pages are report properties that are available at run time and can be included on the report.

But consider the value of adding other report properties on the report. Most of the report properties can be added to unbound text boxes as long as the property is enclosed in square brackets. For the most part, these properties are only of value to you as the developer, but they may also be useful to your users.

For example, the report's Name, Record Source, and other properties are easily added the same way. Figure 21.29 demonstrates how unbound text boxes can deliver this information to a report footer or some other place on the report.

The inset in the lower part of Figure 21.29 shows the information provided by adding the four text boxes to this report. Very often, the user is not even aware of the name of a report—the only text the user sees associated with reports is the text that appears in the title bar (in other words, the report's Caption property). If a user is having problems with a report, it might be helpful to display the information you see in Figure 21.29 in the report footer.

### Adding the user's name to a bound report

An unbound text box with its Control Source set to an unresolved reference will cause Access to pop up a dialog box requesting the information necessary to complete the text box. For example, an unbound text box with its Control Source set to the following displays the dialog box you see in the middle of Figure 21.30 when the report is run:

```
=[What is your name?]
```

### FIGURE 21.29

rptMoreInfo demonstrates how to add more information to your reports.

![](img/1e45673ab6eca9d20e67635ff5b9b318_732_0.png)

### FIGURE 21.30

Use an unbound text box to capture useful information.

![](img/1e45673ab6eca9d20e67635ff5b9b318_732_1.png)

Access displays a similar Parameter dialog box for each parameter in a parameter query. The text entered into the text box is then displayed on the report. (rptUserName in Chapter21.accdb on this book's companion website demonstrates this technique.)

The unbound text box on the report can be referenced by other controls on the report. The Enter Parameter Value dialog box appears before the report is prepared for printing, which means that the data you enter into the dialog box can be used in expressions, calculations, or the VBA code behind the report.

### Adding Even More Flexibility

As you've probably discovered by now, reporting in Access is a very large topic. We've included a few additional techniques that will help you make your reports even more flexible to users.

### Displaying all reports in a combo box

The names of all the top-level database objects are stored in the MSysObjects system table. You can run queries against MSysObjects just as you can run queries against any other table in the database. It's easy to fill a combo box or list box with a list of the report objects in an Access database.

Choose Table/Query as the Row Source Type for the list box and put this SQL statement in the Row Source of your list box to fill the box with a list of all reports in the database:

```
SELECT DISTINCT [Name] FROM MSysObjects
WHERE [Type] = -32764
ORDER BY [Name];
```

The -32764 identifies report objects in MSysObjects, one of the system tables used by Access. The results are shown in Figure 21.31.

Tip
VBA includes the ENVIRON() function, which can be used to get the user's name automatically. Use ENVIRON("USERNAME") in a VBA function and refer to that function in a text box's Control Source to display the user's name without prompting for it. The username returned by ENVIRON() is easily changed by the user, so don't use it where identity is critical.

Note
Reports don't have to be open for this technique to work. MSysObjects knows all the objects in the database, so no reports will escape detection using this technique.

If you're using a naming convention for your database objects, use a prefix to show only the reports you want. The following code returns only those reports that begin with tmp:

```
SELECT DISTINCTROW [Name] FROM MSysObjects
WHERE [Type] = -32764 AND Left([Name], 3) = "tmp"
ORDER BY [Name];
```

Because MSysObjects stores the names of all database objects, you can return the names of the other top-level database objects as well. Just substitute the -32764 as the type value in the preceding SQL statement with the Table 21.3 values to return different database object types.
