A consequence of adding the asterisk to the parameter is that, if the user doesn't enter a parameter value, the criteria evaluates to "LIKE *", and the query returns all records except the nulls. Leaving the asterisk out of the criteria expression results in no returned records if the user fails to provide a product category.

Figure 29.9 shows the Query Parameters dialog box (opened by right-clicking the query's upper area and selecting Parameters from the shortcut menu). You use the Query Parameters dialog box to specify parameters that require special consideration, such as date/time entries or specially formatted numbers. One text entry has been entered in the Query Parameters dialog box to show how it works. You enter the parameter text and choose the parameter's data type.

# FIGURE 29.9

The Query Parameters dialog box.

![](bbox=[0.22, 0.55, 0.78, 0.8])

> TIP
> If you want to add more-complex parameters, such as a range of dates, use an expression such as Between [Enter the Start Date] and [Enter the End Date] as a criterion in a date field. This would display two separate parameter dialog boxes and then filter the date value appropriately.

Unfortunately, Access parameter queries don't provide a way to supply default values for parameters. Your best bet is to always include the asterisk in your criteria expression so that if the user closes the parameter dialog box without entering a value, the query will return all records because the criteria expression will resolve to Like "*".