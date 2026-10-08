For example, the publication date cannot be ahead of the current calendar date by more than 180 days, you can add the following check to the Create method:

```
[HttpPost]
public ActionResult Create(Book newBook)
{
    if (newBook.Published != null &&
        newBook.Published.Value - DateTime.Now).TotalDays > 180)
    {
        ModelState.AddModelError("Published",
            "A future publication date cannot be more than 180 days");
    }
    if (ModelState.IsValid)
    {
        try
        {
            using (var context = new AcmeLibraryDataEntities())
            {
                context.AddToBooks(newBook);
                context.SaveChanges();
            }
            return RedirectToAction("Index");
        }
        catch (Exception)
        {
            return View(newBook);
        }
    }
    return View(newBook);
}
```

As you see, the validation check precedes checking for ModelState.IsValid.

# Displaying Validation Issues

By default, the view generated with the Add View command contains a placeholder for a validation summary, as the following code extract (Create.aspx) shows: