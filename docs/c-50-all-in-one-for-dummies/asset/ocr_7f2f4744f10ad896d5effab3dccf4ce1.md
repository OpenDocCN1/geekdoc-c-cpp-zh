# Data Binding 695

That's all well and good, but if you don't want to show the ID or want
to put the columns someplace to your liking? You can do that, too; just
takes a little more effort.

The capability of the gridview to automatically show all columns in a table
is handled by a property: AutoGenerateColumns. The first thing you need
to do is to set that to False. This tells ASP.NET that you're going to set all the
columns by hand.

Next, you have to tell C what columns you're using. This can be in the
ASP.NET code, this is a C# book, so do it in the C# code.

You need to add two columns to the grid —Say Channel and Episode. In
to order to this, you need to define and set up BoundColumn objects.
You need to add them to the grid. That's what happens under
sheets when you add a datacol tag in the markup.

Here's the resulting markup. I bolded the lines of code that I added to the
 event handler

```
List-Show = new List<>();nprotected void Page_Load(object sender, EventArgs e)
{
Show.Add(ID = 1, Channel = 5, EpisodeTitle = "ASP.NET
Datatabinding", ScheduledTime = new DateTime(2009, 4, 12, 0, 0), ShowTitle
 = "C# Show");
Show.Add(ID = 2, Channel = 5, EpisodeTitle = "ASP.NET
Styling", ScheduledTime = new DateTime(2009, 4, 13, 0, 0), ShowTitle =
 = "C# Show");
Show.Add(ID = 3, Channel = 8, EpisodeTitle = "ASP.NET
Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0), ShowTitle =
 = "C# Show");
Show.Add(ID = 4, Channel = 8, EpisodeTitle = "Partial
Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0), ShowTitle =
 = "C# Show");
Show.Add(ID = 5, Channel = 8, EpisodeTitle = "Operator
Overloading", ScheduledTime = new DateTime(2009, 4, 18, 9, 0), ShowTitle =
 = "C# Show");
GridView1.DataSource = source;
GridView1.AutoGenerateColumns = false;
BoundField channelColumn = new BoundField();
channelColumn.DataField = "channel";
channelColumn.HeaderText = "channel";
GridView1.Columns.Add(channelColumn);
BoundField episodeColumn = new BoundField();
episodeColumn.DataField = "EpisodeTitle";
episodeColumn.HeaderText = "Episode";
GridView1.Columns.Add(episodeColumn);
Page.DataBind();
```

![](bbox=[0.863, 0.323, 0.958, 0.533])