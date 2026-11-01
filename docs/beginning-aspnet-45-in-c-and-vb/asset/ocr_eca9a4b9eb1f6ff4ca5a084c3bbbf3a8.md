Note that there is a subtle difference between adding the handler using Markup View and Design View if you're using VB.NET. If you use Markup View, the handler is added to the markup (OnCheckedChanged="CheckBox1_CheckedChanged") and code is added to the Code Behind. When you use Design View, the code in Markup View is not affected, and the code in the Code Behind is annotated with the Handles keyword to indicate which event (for instance, the click on a button, the check changed event of a check box, and so on) the code responds to. At run time, however, there is no difference.

7. Next, add the following bolded line within the handler code that VS added for you:

```
VB.NET
Protected Sub CheckBox1_CheckedChanged(sender As Object, e As EventArgs)
    Panel1.Visible = CheckBox1.Checked
End Sub
```

```
C#
protected void CheckBox1_CheckedChanged(object sender, EventArgs e)
{
    Panel1.Visible = CheckBox1.Checked;
}
```

8. Save all your changes and then request the page in the browser by pressing Ctrl+F5.

9. When the page first loads, all you see is the check box and the text beside it. When you look at the HTML for the page in the browser (right-click the page and choose View Source or View Page Source depending on your browser), you'll only see the check box; there's no code for the Panel control at this stage sent to the browser. When you click the check box to place a checkmark in it, the page reloads and now shows the text you entered in step 5.

> **WARNING** *If nothing happens, go back to the source of the page in VS and ensure that AutoPostBack is set to True on the CheckBox control.*

If you look at the HTML in the browser, you'll see that the text you typed in step 5 is wrapped in a <div> element with an id of Panel1:

```
<div id="Panel1">
    I am visible now
</div>
```

# How It Works

In step 4 of this exercise you set the Visible property of the Panel control to False. This means that when the page loads, the control is not visible on the server and thus its HTML never makes it to the browser. When you then check the check box, a postback occurs, which sends the information contained in the form to the server. At the server, some code is run that is fired whenever the check box changes its state from checked to unchecked or vice versa. Inside that code block, the following code is executed (shown in C#):

```
Panel1.Visible = CheckBox1.Checked;
```