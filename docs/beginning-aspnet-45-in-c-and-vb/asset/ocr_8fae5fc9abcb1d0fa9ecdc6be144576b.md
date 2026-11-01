Because the review needs a CreateDateTime and an UpdateDateTime, this code sets both. Notice how the UpdateDateTime is filled with the CreateDateTime so both contain the exact same date and time, indicating the item hasn't been modified yet.

If the _id variable did contain a review ID (which means an existing review is being edited and saved), it's queried from the database with a LINQ to Entities query:

```
VB.NET
myReview = (From r In myEntities.Reviews
Where r.Id = _id
Select r).Single()
myReview.UpdateDateTime = DateTime.Now
```

```
C#
myReview = (from r in myEntities.Reviews
where r.Id == _id
select r).Single();
myReview.UpdateDateTime = DateTime.Now;
```

Whether or not an ID was passed to this page, at this stage, the myReview variable contains a Review instance. The remaining code then fills the review's properties by retrieving them from the relevant form controls. For the genre, the code directly assigns the GenreId property instead of querying a complete Genre instance and assigning it to the Genre property of the Review instance. This works because the model has support for foreign key columns, as you learned in the preceding chapter.

Finally, when the object is fully set up, the code calls SaveChanges on the PlanetWroxEntities object. This eventually sends a SQL INSERT or UPDATE instruction to the database to tell it to insert a new or update the existing Review row. Just as with the data source control, calling SaveChanges may throw an error. Chapter 18 digs deeper into handling errors that may occur in your code. After SaveChanges has been called, the user is redirected to the Reviews.aspx page using Response.Redirect:

```
VB.NET
myEntities.SaveChanges()
Response.Redirect("Reviews.aspx")
```

```
C#
myEntities.SaveChanges();
Response.Redirect("Reviews.aspx");
```

Obviously, once you've saved a review in the database, you can edit it again. Once you click one of the existing reviews in the reviews list at Reviews.aspx, you're taken to the Add/Edit page with the ID of the review in the query string. For example, browsing to http://localhost:1049/Management/AddEditReviewHandCoded.aspx?id=6 enables me to edit the Death Magnetic album by Metallica. The page is able to detect the ID in the query string using this code in Page_Load:

```
VB.NET
If Not String.IsNullOrEmpty(Request.QueryString.Get("Id")) Then
_id = Convert.ToInt32(Request.QueryString.Get("Id"))
End If
```