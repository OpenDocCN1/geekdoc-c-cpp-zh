# Immediate Solutions

Normally, when you build dynamic Web sites, you might want to post one page to another page with some information. This can be understood better by taking an example of an online banking Web site that collects different types of information on each page. In this case, you can configure certain controls, such as a button on a page, and post it to a different target page so that when users click the button, they see the information on the targeted page. This is referred to as cross-page posting.

Now, let's take the same application named FileSystemWebsite (available in the CD-ROM as well) to learn about both postback and cross-pages posting. You should have at least two Web Pages in the application. In this example, you have two Web Pages–Default and Marks. When users enter their roll number and name in the Default Web page and click the Show Marks button, they are redirected to the Marks.aspx Web page. However, the Marks page is blank. You need to display some marks based on the roll number entered by the user in the Default page. For this, you need cross-page posting. To do so, perform the following steps:

+   1. Add the code given in Listing 13.13 which shows the Source view of the Default Web page that implements the cross-page posting:

```
<%@ Page Language="C#" AutoEventwireup="true" CodeFile="Default.aspx.cs" %>
<\%@ Page ... (full code block from image) ...
</form>
</body>
</html>
```

Listing 13.13: The Complete Code for Default.aspx