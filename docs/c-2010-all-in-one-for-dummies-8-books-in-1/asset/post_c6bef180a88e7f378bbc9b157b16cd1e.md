
# Data Binding 675

```csharp
shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle = 'Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0), ShowTitle = "Learning C#") ;
shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle = 'Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0), ShowTitle = "Learning C#") );
```

## 6. Add the datasource and the databind at the bottom of the page load.

I have bonded the lines that I added in the code:

```csharp
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show (ID = 1, Channel = 5, EpisodeTitle = '*ASP.NET Binding', ScheduledTime = new DateTime(2009, 4, 12, 13, 0), ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 2, Channel = 5, EpisodeTitle = '*ASP.NET Styling', ScheduledTime = new DateTime(2009, 4, 12, 13, 0), ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 3, Channel = 8, EpisodeTitle = '*Inheritance', ScheduledTime = new DateTime(2009, 4, 16, 9, 0), ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle = '*Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0), ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle = '*Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0), ShowTitle = "Learning C#"));
    Gridview1.DataSource = shows;
    Page.DataBind();
}
```

## 7. Refresh <F5> to see the application run.

As you can see in Figure 3-6, the controls from the database are auto-bound to the HTML grid.

That's all well and good, but what if you don't want to show the ID, or want to bind the columns somewhere to your liking? You can do that, but it takes a little more effort.

The capability of the gridview to automatically show all columns in a table is handled by a property: AutoGenerateColumns. The first thing we need to do is set it to False. This tells ASP.NET we are going to get all of the columns by hand.

Next, we need to tell what columns we are using. This can be done in the ASP.NET code, but this is a C# code. Let's do it in the C# code.

We need to add columns to the grid - let say Channel and Episode. In order to do this, we need to define and set two BoundColumn objects. Then we need to add to the grid. That happens under the scenes when we add a datacolumn tag in the markup.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_700_0.png)

# 676 Data Binding

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_701_0.png)

Figure 3-6: The TV schedule Columns here are bound to the grid.

Here's the resulting markup. I bolded the lines of code that I added to the page event handler:

```csharp
List<Show> show = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    show.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET DataBinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "ASP.NET Styling", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 19, 0, 0), ShowTitle = "C# Show" });
}
```

```csharp
GridView.DataSource = show;
GridView.AutoGenerateColumns = false;

BoundField channelColumn = new BoundField();
channelColumn.DataField = "Channel";
channelColumn.HeaderText = "Channel";
GridView.Columns.Add(channelColumn);

BoundField episodeColumn = new BoundField();
episodeColumn.DataField = "EpisodeTitle";
episodeColumn.HeaderText = "Episode";
GridView.Columns.Add(episodeColumn);

Page.DataBind();
```

# Styling Your Controls

When you have the data in your controls, you need to get the control looking a certain way. There are a lot of options here. All the controls with properties can be set at design time and at runtime, or bound to cascading stylesheets (CSS).

Being able to style is necessary; being able to manage the styles at runtime with C# is near magic. Using a combination of the methods makes it possible to create dynamic applications that give the user the best experiences.

## Styling control properties

By far, the simplest way to style a control is to use the built-in properties. You know exactly what you are applying, and IntelliSense helps you do so. Notice I didn't say it was the “best” way. I said it was simplest.

Setting control properties has a host of problems. If you have more than one control to set up, you have the properties on each of them — even if they are the same. It makes your code messy.

Sometimes, you need to set style this way. The best way to see all is to check the Properties panel, as shown in Figure 3-7. If you actually set properties here, it will be in the markup, not the code-behind, but you can find the names.

```asp
<asp:GridView ID="GridView1" runat="server" OnSelectedIndex="GridView1_SelectedIndex" RowStyle="#CCCCCC" />
```

After you get the name of something you want to set, you just set it like any other property:

```csharp
GridView1.RowStyle.BackColor = System.Drawing.Color.Red;
```

The roughest part is discovering what framework element the style will want as a value. The easiest way to determine this is to type the part to the left of the equal sign, and then mouse over the property to see how it is declared. BackColor, for instance, requires a System.Drawing.Color element. When I discovered that, I knew where to go to get the value.

![](img/36596fb11aa4233d5cab0d6ddd1d82e_702_0.png)

# 678 Styling Your Controls

![](img/36596fb11aa4233d5cab0d6ddd1d82e_703_0.png)

Figure 3-7: Styles in the Properties panel.

## Binding styles with CSS

Because in a Web application using Cascading Style Sheets (CSS) seems like a good approach to handle our styles. To start, you need a few CSS classes, which are not the same as .NET classes. A CSS is a collection of styles that can be connected to markup, so as to match the properties between. To bind styles with CSS, follow these steps:

1. Right-click the project and select Add New.
2. Select Style Sheet from the dialog box. I named it Chapter3.css.
3. When the style sheet comes up, right-click the CSS Outline and select Add Rule.
4. In the element dialog box, select Class Name and type GridViews in the text box.
5. Click the right arrow button as shown in Figure 3-8.
6. Press OK, and notice the new entry in the style sheet.

# 679 Making Sure the Site Is Accessible

![](img/36596fb11aa4233d5cab0d6ddd1d82e_704_0.png)

Figure 3-8: Adding a style sheet class.

Just for demonstration, I added a few things to the style sheet.

```css
body {
  font-family: 'French Script MT';
  background-color: Fuchsia;
}
```

To bind this to, use the CssClass property, which accepts the class in the CSS file. Link the CSS file to the page in question in the page markup, using the "link" snippet in the ASP.NET markup (remember to put it in the <head> tag section).

In the code-behind, just set the CssClass property like you would any other property, like this:

```csharp
GridView.CssClass = "GridView";
```

# Making the Site Is Accessible

When I say accessible here, I am not talking about the server being up. I am talking about making sure the controls you use are available to people who have disabilities, such as diminished senses of sight, hearing, or touch. Such people have a different browsing experience than you or I.

Microsoft has made a significant investment in accessibility browsing, and you'll be pleased to find that most of the controls make good decisions about accessibility out of the box. Understanding how to use them for this purpose takes a little effort, however.
