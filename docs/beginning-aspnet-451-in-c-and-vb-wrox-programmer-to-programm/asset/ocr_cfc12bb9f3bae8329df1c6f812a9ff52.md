If you were using validation controls (and you really should, as you learned in Chapter 9), you need to check whether or not the page is valid before you proceed with saving the Review instance:

# VB.NET

```
Protected Sub SaveButton_Click(sender As Object, e As EventArgs) _
    Handles SaveButton.Click
If (Page.IsValid) Then
    Using myEntities As New PlanetWroxEntities()
```

# C#

```
protected void SaveButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
```

This is really all there is to adding and editing new reviews using your own code against the Entities Framework. I realize it may look a little funky at first because you need to reset your head, forget about smart controls and their many properties and events, and think in straight code. However, EF makes this pretty straightforward, and most of it comes down to querying entities, copying values from or to an object’s properties, and calling SaveChanges to propagate the changes back to the database.

Clearly, this is just the beginning. There’s a whole lot more you can do once you start writing your own code, whether or not it targets EF. For more information, get yourself a copy of Programming Entity Framework Second Edition by Julia Lerman or Professional ASP.NET 4.5 in C# and VB from Wrox (ISBN: 978-1-118-31182-0).

In all the database examples you have seen so far, the code accesses the database for each and every request. Every time some data needs to be displayed, it’s retrieved fresh from the database. Clearly, this can be a waste of time and resources like network bandwidth and CPU cycles, especially if the data hasn’t changed since the last time you accessed it. In the final section of this chapter, you are introduced to a technique called caching that can greatly improve the responsiveness and performance of your application.

# CACHING

Caching is one of the best and often easiest ways to improve the performance of an application. It’s also an option that is too often overlooked by developers. With caching, a copy of your data is stored in a location that can be accessed very quickly. The idea with caching is that fetching data from the cache should be faster than regenerating it or fetching it from the original data source. Therefore, most caching solutions store data in memory, which is usually the fastest way to get the data. The .NET cache is no exception, and enables you to store frequently accessed data in a special location in the computer’s memory.

Typically, the caching principle takes the route displayed in Figure 15-15.