
(continued)

| TEMPLATE | APPLIES TO | DESCRIPTION |
|---|---|---|
| `<EmptyDataTemplate>` | GridView, DetailsView, FormView, ListView | Used to display empty items — for example, when no records are available in a GridView |
| `<PagerTemplate>` | GridView, DetailsView, FormView | Used to format pagination |
| `<GroupTemplate>` | ListView | Used to specify the output surrounding groups of items |
| `<GroupSeparatorTemplate>` | ListView | Used between groups of items |
| `<EmptyItemTemplate>` | ListView | When using item groups, used to supply output for empty items in a group. This template is used when there are not enough items in a group to fill the group. |

The easiest way to understand how to use these is through an example.

## Using Templates

You will extend the table at the top of the Default.aspx page of PCSWebSite2 to contain a ListView displaying each of the events stored in the database. You will make these events selectable such that details of any event can be displayed by clicking on its name, in a FormView control.

First, you need to create new data sources for the data-bound controls. It is good practice (and strongly recommended) to have a separate data source for each data-bound control.

The SqlDataSource control required for the ListView control, MRBEEventData2, is similar to MRBEEventData, except that it needs to return only Name and ID data. The required code is as follows:

```asp
<asp:SqlDataSource ID="MRBEEventData2" runat="server"
SelectCommand="SELECT [ID], [Name] FROM [Events]"
ConnectionString="<%$ ConnectionStrings:MRBConnectionString %>">
</asp:SqlDataSource>
```

The data source for the FormView control, MRBEEventDetailData, is more complicated, although you can build it easily enough through the data source Configuration Wizard. This data source uses the selected item of the ListView control, which you will call EventList, to get only the selected item data. This is achieved using a parameter in the SQL query, as follows:

```
<tr>
<td align="center" colspan="3">
<asp:ValidationSummary ID="validationSummary" runat="server"
HeaderText="Before submitting your request:" />
</td>
</tr>
<tr>
<td align="left" colspan="3" style="width: 40%;">
<table cellspacing="4" style="width: 100%;">
<tr>
<td colspan="2" style="text-align: center;">
<h2>Event details</h2>
</td>
</tr>
<tr>
<td style="width: 40%; background-color: #ccffcc;"
valign="top">
<asp:ListView ID="EventList" runat="server"
DataSourceID="MRBEventData" DataKeyNames="ID"
OnSelectedIndexChanged="EventList_SelectedIndexChanged">
<LayoutTemplate>
<ul>
<asp:PlaceHolder ID="itemPlaceholder"
runat="server" />
</ul>
</LayoutTemplate>
<ItemTemplate>
<li>
<asp:LinkButton Text="<%# Bind("Name") %>"
runat="server" ID="NameLink" CommandName="Select"
CommandArgument="<%# Bind("ID") %>"
CausesValidation="false" />
</li>
</ItemTemplate>
<SelectedItemTemplate>
<li>
<b><%# Eval("Name") %></b>
</li>
</SelectedItemTemplate>
</asp:ListView>
</td>
<td valign="top">
<asp:FormView ID="FormView1" runat="server"
DataSourceID="MRBEventDetailData">
<ItemTemplate>
<h3><%# Eval("Name") %></h3>
<b>Date:</b>
<%# Eval("EventDate", "{0:D}") %>
<br />
<b>Room:</b>
<%# Eval("Room") %>
<br />
<b>Attendees:</b>
<%# Eval("AttendeeList") %>
</ItemTemplate>
</asp:FormView>
</td>
</tr>
</table>
</td>
</tr>
</table>
```

Here you have added a new table row containing a table with a ListView control in one column and a FormView control in the other.

The ListView uses <LayoutTemplate> to output a bulleted list and <ItemTemplate> and <SelectedItemTemplate> to display event details as list items. In <LayoutTemplate>, a container element for items is specified with a PlaceHolder control that has the ID="itemPlaceholder" attribute. To facilitate selection, you raise a Select command from the event name link rendered in <ItemTemplate>, which automatically changes the selection. You also use the OnSelectedIndexChanged event, triggered when the Select command changes the selection, to ensure that the list display updates itself to display the selected item in a different style. The event handler for this is shown in the following code:

```
protected void EventList_SelectedIndexChanged(object sender, EventArgs e)
{
    EventList.DataBind();
}
```

You also need to ensure new events are added to the list:

```
if (queryResult == 1)
{
    resultLabel.Text = "Event Added.";
    EventData = null;
    calendar.SelectedDate =
        GetFreeDate(calendar.SelectedDate.AddDays(1));
    GridView1.DataBind();
    EventList.DataBind();
}
```

Now selectable event details are available in the table, as shown in Figure 40-14.

There is much more that you can do with templates and data-bound controls in general, enough in fact to fill a whole book. However, this should be enough to get you started with your experimentation.

![](img/d7d2ffa0a76feaab821930e95daace93_1241_0.png)

FIGURE 40-14

## APPLICATION CONFIGURATION

Throughout this chapter, we have alluded to the existence of a conceptual application containing web pages and configuration settings. This is an important concept to grasp, especially when configuring your web site for multiple concurrent users.

A few notes on terminology and application lifetime are necessary here. An *application* is defined as all files in your project, and is configured by the *web.config* file. An *Application* object is created when an application is started for the first time, which will be when the first HTTP request arrives. Also at this time, the *Application_Start* event is triggered and a pool of *HttpApplication* instances is created. Each incoming request receives one of these instances, which performs request processing. Note that this means *HttpApplication* objects do not need to cope with concurrent access, unlike the global *Application* object. When all *HttpApplication* instances finish their work, the *Application_End* event fires and the application terminates, destroying the *Application* object.

The event handlers for the events mentioned earlier (along with handlers for all other events discussed in this chapter) can be defined in a *global.asax* file, which you can add to any web site project (it is listed as Global Application Class in the templates when you see that you can add a new item to a web application). The generated file contains blanks for you to fill in; for example:

```
void Application_Start(Object sender, EventArgs e)
{
    // Code that runs on application startup
}
```

When an individual user accesses the web application, a *session* is started. Similar to the application, this involves the creation of a user-specific *Session* object, along with the triggering of a *Session_Start* event. Within a session, individual requests trigger *Application_BeginRequest* and *Application_EndRequest* events. These can occur several times during the scope of a session as different resources within the application are accessed. Individual sessions can be terminated manually, or will time out if no further requests are received. Session termination triggers a *Session_End* event and the destruction of the *Session* object.

Against the background of this process, you can do several things to streamline your application. If all instances of your application use a single, resource-heavy object, for example, then you might consider instantiating it at the application level. This can improve performance and reduce memory usage with multiple users because in most requests no such instantiation will be required.

Another technique you can use is to store session-level information for use by individual users across requests. This might include user-specific information that is extracted from a data store when the user first connects (in the *Session_Start()* event handler), and is made available until the session is terminated (through a timeout or user request).

These techniques are beyond the scope of this book — and you might want to consult *Professional ASP.NET 4: in C# and VB* (Wiley Publishing, Inc., 2010, ISBN 978-0470-502204) for details — but it helps to have a broad understanding of the processes.

Finally, you need to look at *web.config* files. A web site will usually have one of these in its root directory (although it is not created for you by default), and may have additional ones in subdirectories to configure directory-specific settings (such as security). The PCSWebSite web site developed in this chapter received an auto-generated Web.config file when you added a stored database connection string, which you can see in the file:

```
<connectionStrings>
  <add name="MyConnectionString" connectionString="Data Source=.\SQLEXPRESS;AttachDbFilename=|DataDirectory|\MeetingRoomBooker.mdf;Integrated Security=True;User Instance=True" providerName="System.Data.SqlClient" />
</connectionStrings>
```
