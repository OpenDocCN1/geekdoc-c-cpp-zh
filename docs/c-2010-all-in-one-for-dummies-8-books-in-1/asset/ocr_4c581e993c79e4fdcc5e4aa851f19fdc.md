# Data Binding 675

```
shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle =
'Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0),
ShowTitle = "Learning C#"));
shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle =
'Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0), ShowTitle = "Learning C#")
```

# 6. Add the datasource and the databind at the bottom of the page load.

I have bonded the lines that I added in the code:

```
List-Show = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show (ID = 1, Channel = 5, EpisodeTitle =
'*ASP.NET Binding', ScheduledTime = new DateTime(2009, 4, 12, 13, 0),
ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 2, Channel = 5, EpisodeTitle =
'*ASP.NET Styling', ScheduledTime = new DateTime(2009, 4, 12, 13, 0),
ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 3, Channel = 8, EpisodeTitle =
'*Inheritance', ScheduledTime = new DateTime(2009, 4, 16, 9, 0),
ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle =
'*Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0),
ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle =
'*Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0),
ShowTitle = "Learning C#")
    Gridview1.DataSource = shows;
    Page.DataBind();
}
```

# 7. Refresh <F5> to see the application run.

As you can see in Figure 3-6, the controls from the database are auto-bound to the HTML grid.

That's all well and good, but what if you don't want to show the ID, or want to bind the columns somewhere to your liking? You can do that, but it takes a little more effort.

The capability of the gridview to automatically show all columns in a table is handled by a property: AutoGenerateColumns. The first thing we need to do is set it to False. This tells ASP.NET we are going to get all of the columns by hand.

Next, we need to tell what columns we are using. This can be done in the ASP.NET code, but this is a C# code. Let's do it in the C# code.

We need to add columns to the grid - let say Channel and Episode. In order to do this, we need to define and set two BoundColumn objects. Then we need to add to the grid. That's happens under the sheets when we add a datacolumn tag in the markup.

![](bbox=[0.863, 0.325, 0.966, 0.533])