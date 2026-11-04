# 7. In the body of the if statement, have the FileUpload control help us save the file.

New code is in bold.

```
```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    String localPath = Server.MapPath("~/UploadedFiles/");
    if (FileUpload1.HasFile)
    {
        try
        {
            FileUpload1.PostedFile.SaveAs(localPath + FileUpload1.FileName);
        }
        catch (Exception ex)
        {
            Response.Write(ex.Message);
        }
    }
}
```
```

This is a nice feature. In the old days, we needed to wrangle the bytes themselves. Uphill both ways, in the snow.

To build a comprehensive file upload function, you need a little more stringent programming practices. (Like my error handling, for instance?) The idea here, though, is that there is a FileUpload control that gives us significant back-end control.

While we are here, take a look at the HttpFileCollection, which is the System.Web class that gives the FileUpload control its power. All the properties of the FileUpload control, like the file's bits, name, and all that, are in the HttpFileCollection. Check it out if you need more fine-grained control than the FileUpload control gives you.

# Baking Cookies

Cookies are the only thing that a Web site can directly save on a client machine without the client's direct permission. It still requires the indirect permission, because a user can disable cookies, but passively a cookie can be saved without actually asking the user, "Is it okay if I save this?"

Cookies are useful for state management. If you know the ID of the client's shopping cart, for instance, you can save that ID in a cookie, and even if the client goes away for a week and comes back, you still will be able to go back to the business layer and look up the information.