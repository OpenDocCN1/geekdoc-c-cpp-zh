Another resizing technique is to position the cursor over any of the sizing handles on a selected control and double-click. The control automatically "sizes to fit" the text contained within the control. This quick method can also be used to align not only labels but also text boxes to the grid.

# Adding Data

When you're looking at data through forms, you can usually assume that the data is current. However, with printed reports, you don't always know how old the data is. Adding little touches like when the report was printed can help increase the confidence the user has in the report. This section shows you some techniques that enable you to add additional information to the report to let the users know something of its origin.

# Adding more information to a report

You probably know that the following expression in an unbound text box prints the current page and the number of pages contained in the report:

```
="Page " & [Page] & " of " & [Pages]
```

Both Page and Pages are report properties that are available at run time and can be included on the report.

But consider the value of adding other report properties on the report. Most of the report properties can be added to unbound text boxes as long as the property is enclosed in square brackets. For the most part, these properties are only of value to you as the developer, but they may also be useful to your users.

For example, the report's Name, Record Source, and other properties are easily added the same way. Figure 21.29 demonstrates how unbound text boxes can deliver this information to a report footer or some other place on the report.

The inset in the lower part of Figure 21.29 shows the information provided by adding the four text boxes to this report. Very often, the user is not even aware of the name of a report—the only text the user sees associated with reports is the text that appears in the title bar (in other words, the report's Caption property). If a user is having problems with a report, it might be helpful to display the information you see in Figure 21.29 in the report footer.

# Adding the user's name to a bound report

An unbound text box with its Control Source set to an unresolved reference will cause Access to pop up a dialog box requesting the information necessary to complete the text box. For example, an unbound text box with its Control Source set to the following displays the dialog box you see in the middle of Figure 21.30 when the report is run:

```
=[What is your name?]
```