
The most interesting thing here is how you access the connection string you created earlier, using the following syntax:

```
ConfigurationManager.ConnectionStrings["MRBConnectionString"].ConnectionString
```

The ConfigurationManager class (which requires a namespace import for System.Configuration) gives you access to all assorted configuration information, all stored in the Web.config configuration file for your web application. You will look at this in more detail later in this chapter.

After you have created your SQL command, you can use it to insert the new event:

```
conn.Open();
int queryResult = insertCommand.ExecuteNonQuery();
conn.Close();
```

ExecuteNonQuery() returns an integer representing how many table rows were affected by the query. If this is equal to 1, your insertion was successful. If so, put a success message in resultLabel, clear EventData because it is now out of date, and change the calendar selection to a new, free date. Because GetFreeDate() involves using EventData, and the EventData property automatically refreshes itself if it has no data, the stored event data will be refreshed:

```
if (queryResult == 1)
{
    resultLabel.Text = "Event Added.";
    EventData = null;
    calendar.SelectedDate =
    GetFreeDate(calendar.SelectedDate.AddDays(1));
}
```

If ExecuteNonQuery() returns a number other than 1, you know that there has been a problem. The code in this example throws an exception if a number other than 1 is returned. This exception is caught by the general catch block for the database access code.

This catch block simply displays a general failure notification in resultLabel:

```
else
{
    throw new System.Data.DataException("Unknown data error.");
}
catch
{
    resultLabel.Text = "Event not added due to DB access "
        + "problem.";
}
```

This completes your data-aware version of the event-booking application.

## More on Data Binding

As mentioned earlier in this chapter, the available web server controls include several that deal with data display (GridView, DataList, DetailsView, FormView, and Repeater). These are all extremely useful when it comes to outputting data to a web page because they perform many tasks automatically that would otherwise require a fair amount of coding.

First, you will look at how easy using these controls can be, by adding an event list display to the bottom of the display of PCSWebSite3.

Drag a GridView control from the toolbox to the bottom of Default.aspx, and select the MRSEventData data source you added earlier for it, as shown in Figure 40-12.

Next, click Refresh Schema, and that's all you need to do to display a list of events under the form — try viewing the web site now and you should see the events, as shown in Figure 40-13.

![](img/d7d2ffa0a76feaab821930e95daace93_1237_0.png)

FIGURE 40-12

| ID | Name | Room | AttendeeList | EventDate |
|---|---|---|---|---|
| 1 | My Birthday | 4 | Iggy Pop (5), Sean Connery (7), Albert Einstein (10), George Clooney (14), Jules Verne (18), Robin Hood (20), and Kurt Watson | 17/09/2010 00:00:00 |
| 2 | Dinner | 1 | Bill Gates (1), Monika Lewinsky (2), and Bruce Lee | 15/06/2010 00:00:00 |
| 3 | Discussion of darkness | 6 | Vlad the Impaler (4), Moya Hindley (13), and Bedelbud | 29/10/2010 00:00:00 |
| 4 | Christmas with P... | 9 | Dr Frank N Parter (11), Bobby Davro (15), John F Kennedy (16), Stephen Kang (19), and Karth Watson | 25/12/2010 00:00:00 |
| 5 | Escape | 17 | Monika Lewinsky (2), Stephen King (19), and Spartacus | 10/05/2010 00:00:00 |
| 6 | Planetary Conquest | 14 | RB Gates (1), Albert Einstein (10), Dr Frank N Parter (11), Bobby Davro (15), and Darth Vader | 15/06/2010 00:00:00 |
| 7 | Homecoming Celebration | 7 | William Shakespeare (6), Christopher Columbus (12), Robin Hood (20), and Ulysses | 22/06/2010 00:00:00 |
| 8 | Dalek Reunion Ball | 12 | Roger Moore (8), George Clooney (14), Bobby Davro (15), and Davros | 12/06/2010 00:00:00 |
| 9 | Romantic meal for two | 13 | George Clooney (14), and Donna Watson | 29/09/2010 00:00:00 |

FIGURE 40-13

You can also make one further modification in submitButton_Click() to ensure that this data is updated when new records are added:

```
if (queryResult == 1)
{
    resultLabel.Text = "Event Added.";
    EventData = null;
    calendar.SelectedDate =
    GetFreeDate(calendar.SelectedDate.AddDays(1));
    GridView1.DataBind();
}
```

All data-bindable controls support this method, which is normally called by the form if you call the top-level (this) DataBind() method.

You probably noticed in Figure 40-13 that the date/time display for the EventDate field is a little messy. Because you are looking at dates only, the time is always 00:00:00 AM — information that isn't really necessary to display. In the next sections, you see how this date information can be displayed in a more user-friendly fashion in the context of a ListView control. As you might expect, the DataGrid control contains many properties that you can use to format the displayed data, but I'll leave these for you to discover.

## Data Display with Templates

Many of the data display controls allow you to use templates to format data for display. Templates, in an ASP.NET sense, are parameterized sections of HTML that are used as elements of output in certain controls. They enable you to customize exactly how data is output to the browser, and can result in professional-looking displays without too much effort.

Several templates are available to customize various aspects of list behavior. One of the most important templates is <ItemTemplate>, which is used in the display of each data item in a list for Repeater, DataList, and ListView controls. You declare this template (and all the others) inside the control declaration. For example:

```
<asp:DataList Runat="server" ... >
<ItemTemplate>
</ItemTemplate>
</asp:DataList>
```

Within template declarations, you will normally want to output sections of HTML along with parameters from the data that is bound to the control. You can use a special syntax to output such parameters:

```
<%# expression %>
```

The expression placeholder might be simply an expression binding the parameter to a page or control property, but is more likely to consist of an Eval() or Bind() expression. These functions can be used to output data from a table bound to a control simply by specifying the column. The following syntax is used for Eval():

```
<%# Eval("ColumnName") %>
```

An optional second parameter allows you to format the data returned, which has syntax identical to string formatting expressions used elsewhere. This can be used, for example, to format date strings into a more readable format — something that was lacking in the earlier example.

The Bind() expression is identical but allows you to insert data into attributes of server controls. For example:

```
<asp:Label Runat="server" ID="ColumnDisplay" Text='<%# Bind("ColumnName") %>' />
```

Note that because double quotes are used in the Bind() parameter, single quotes are required to enclose the attribute value.

The following table provides a list of available templates and when they are used.

| TEMPLATE | APPLIES TO | DESCRIPTION |
|---|---|---|
| `<ItemTemplate>` | DataList, Repeater, ListView | Used for list items |
| `<HeaderTemplate>` | DataList, DetailsView, FormView, Repeater | Used for output before item(s) |
| `<FooterTemplate>` | DataList, DetailsView, FormView, Repeater | Used for output after item(s) |
| `<LayoutTemplate>` | ListView | Used to specify output surrounding items |
| `<SeparatorTemplate>` | DataList, Repeater | Used between items in list |
| `<ItemSeparatorTemplate>` | ListView | Used between items in list |
| `<AlternatingItemTemplate>` | DataList, ListView | Used for alternate items; can aid visibility |
| `<SelectedItemTemplate>` | DataList, ListView | Used for selected items in the list |
| `<EditItemTemplate>` | DataList, FormView, ListView | Used for items being edited |
| `<InsertItemTemplate>` | FormView, ListView | Used for items being inserted |
