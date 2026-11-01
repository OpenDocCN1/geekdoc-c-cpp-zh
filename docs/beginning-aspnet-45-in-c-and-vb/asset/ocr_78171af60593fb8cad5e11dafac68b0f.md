```
{
    myReview = (from r in myEntities.Reviews
        where r.Id == reviewId
        select r).SingleOrDefault();

    if (myReview != null)
    {
        Cache.Insert(cacheKey, myReview, null, DateTime.Now.AddMinutes(20),
            System.Web.Caching.Cache.NoSlidingExpiration);
    }
}

if (myReview != null)
{
    TitleLabel.Text = myReview.Title;
    SummaryLabel.Text = myReview.Summary;
    BodyLabel.Text = myReview.Body;
    Title = myReview.Title;
    MetaDescription = myReview.Summary;
}
```

6. Open the page All.aspx from the Reviews folder and delete the GridView that you created in the previous chapter. Replace it with a simple Repeater control that contains a single HyperLink into your new details page:

```
<asp:Content ID="Content2" ContentPlaceHolderID="cpMainContent" runat="Server">
    <asp:Repeater ID="Repeater1" runat="server" ItemType="PlanetWroxModel.Review">
        <ItemTemplate>
            <asp:HyperLink ID="HyperLink1" runat="server"
                NavigateUrl='<%# "ViewDetails.aspx?reviewId=" + Item.Id.ToString() %>'
                Text='<%# Item.Title %>'> </asp:HyperLink>
        </ItemTemplate>
        <SeparatorTemplate><br /></SeparatorTemplate>
    </asp:Repeater>
</asp:Content>
```

7. Switch to the Code Behind of the page and replace the last two calls that used the GridView so they end up using the Repeater control instead:

# VB.NET

```
Repeater1.DataSource = allReviews
Repeater1.DataBind()
```

# C#

```
Repeater1.DataSource = allReviews;
Repeater1.DataBind();
```

8. Add the following CSS declaration to the end of the CSS files for the Monochrome and the DarkGrey themes. Since this is a front-end page visited by your users, you don’t need to add it to the Management theme:

```
.Summary
{
```