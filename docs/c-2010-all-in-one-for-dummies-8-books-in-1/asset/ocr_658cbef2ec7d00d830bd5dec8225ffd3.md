```
namespace Chapter_3
{
    public partial class Text : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Labell.Text = "This is some text from the codebehind.";
        }
    }
}
```

# 7. Press <F5> to launch the application.

You'll see that label text by the C# code.

How to decide between labels and text? It's usually easy. Use a label if the text will need to change based on input from the user or use text if the text is static. A description of an item that is loaded from a database? That's a label. Your CEO's bio? That's text.

![](bbox=[0.218, 0.423, 0.845, 0.735])

Figure 3-1:
There is text, and there is text.

# Images

Images are next to text in the realm of standard Web site fare. It's a popular topic because programmers are graphic artists, and making nice images that fit together look good is hard.

Nonetheless, sometimes you just want to show a picture on a page. Just as with text, there are two ways you can do this. (Okay, there are more than two.) You can use the HTML <img> tag, or you can use the ASP.NET Image control.