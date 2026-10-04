
# CHAPTER 4 WORKING WITH ASP.NET SERVER CONTROLS

![](img/9e033e3b9560597824f8b22941d6d8bb_163_0.png)

FIGURE 4-17

+   5. In the first cell of the row, draw a TextBox control.
6. Next, draw Button controls into the control grid of the first two rows of the table.
7. Click the Button in the first row and press F4 to open the Properties Grid. Set the Button's Text property to Set Date and its ID to SetDate. You'll find the ID property all the way to the end of the list with properties, or at the beginning if you have properties sorted alphabetically.
8. Repeat for the other button or call it PlainPostback and set its Text property to Plain Postback. When you're done, the page should look like Figure 4-18 in Design View.

![](img/9e033e3b9560597824f8b22941d6d8bb_163_1.png)

FIGURE 4-18

+   9. Double-click the Set Date button in Design View and add the following bolded code on the empty line between the code lines you inserted for:

```
VB.NET
Protected Sub SetDate_Click(sender As Object
```

```
C#
protected void SetDate_Click(object sender, EventArgs e)
{
    Label.Text = DateTime.Now.ToString();
}
```

There's no need to write code for the Label Postback button.

+   10. Open the page in the browser by pressing Ctrl+F5. Select a date on the calendar by clicking one of the days. Notice that as you click the date, the page reloads, caused by a postback. You learn more about this in the How It Works section for this exercise.

+   11. Enter text in the TextBox control and then click the Set Date button again. Again the page is posted back to the server and the Label is updated with today's date and each time you click the button. The TextBox shows the text you entered. Wait a few seconds, and then click the Postback button. Again, a postback occurs, and page reloads. Now take a look at the Label. It still contains the date and time that was displayed when you last clicked the Set Date button. Click the Postback button a few times and notice that the Label doesn't change. The TextBox should still display the text you entered.

+   12. Go back to VS and open the Properties Grid for the Label in Design View. Locate the EnableViewState property and set it to False by selecting from the drop-down list or double-clicking the property name or its value. Repeat this for the TextBox control.

+   13. Repeat steps 10 and 11 by replaying the page in the browser and clicking the calendar and the buttons. This time, when you click the Postback button, you'll see that the Label defaults to its initial text: Label. The TextBox, however, still displays the text you entered.

## How It Works

To understand how all this works, you need to look at a few important elements. First, open up the page in the browser and view its HTML source. You can do this by right-clicking the page in the browser and choosing the View Source or View Page menu item. Near the top of the window, you see the following `<form>` element:

```
<form method="post" action="Default.aspx" id="form1">
</form>
```

The HTML `<form>` element is used to submit user information from the browser to the server. A user can enter information using control boxes, drop-down lists, check boxes, and so on. A form can be submitted in two ways: with POST (as in the previous `<form>` element) or with GET. In the former case, all data is added to the body of the request and then sent to the server. In the case of the GET method, all the data is appended to the address of the request. The intricacies of the differences are not important right now; what's important to understand is what the `<form>` element is used for: it encapsulates forms whose values are submitted back to the server en masse.

When a control like a Button is clicked, it causes a postback to the server. During this postback, all the relevant information in the form is submitted back to the server where it can be used to rebuild the page.

# CHAPTER 4 WORKING WITH ASP.NET SERVER CONTROLS

By default, all your ASP.NET Web Forms use the POST method to send data to the server. Also, by default, an ASP.NET page always contains one form. Because this is so common, a page (or Master Page as you learn in Chapter 6) created in VS already contains the <form> element, so you don't have to add it yourself. Finally, it's important to understand that ASP.NET Web Form always submits back to itself. In other web environments, like classic ASP and PHP, it's uncommon to set the action attribute of a second page that then processes the data the user has submitted. However, with an ASP.NET page, you'll find that if you set the action attribute explicitly, the ASP.NET run time will revert it to the name of the current page.

> NOTE ASP.NET supports a feature called Cross Page Postbacks that enables you to submit from one page to another. To learn more about this concept, search the MSDN for Cross Page Postbacks or get yourself a copy of ASP.NET 4.5 from Wm.

The next thing to look at is ASP.NET's State function implemented with the VIEWSTATE field you see in the HTML source in bold in the following:

```
<form method="post" action="State.aspx" id="form1">
  <input type="hidden" name="VIEWSTATE" value="XXrCU251B9YtMD0lC5n2/Yvx5oxG2Ka08XGf3F0/W016/uppieh7Nht1fyr990IRXrKy4pDHHS9BBRucja40PKyWvcXRnBI3KkidqR5AVX96DQE5EL546e8BOFF3ifJ4c3YqtG3zpba=" />
</form>
```

Although it appears to contain nothing more than random characters, it actually contains useful information. To protect the information stored in this field, ASP.NET has converted the page state into an encoded string. If you were able to look inside the value of the fields, you'd find a value for the Label1 with the current date and time.

When your ASP.NET page loads, the ASP.NET run time fills this field with information about the page. For example, it added the value to the Text property of the Label1 when you called a postback by clicking the Set Date button. Similarly, it sets the calendar for the Date control. When the page is submitted by a postback, the value in this hidden __VIEWSTATE field is sent with the request. Then, when ASP.NET creates the new page on the server, the information from the __VIEWSTATE field is read and applied to the controls. This way, a control like the Label is able to maintain its text after the page has been posted back to the server.

The TextBox does not use View State, though. It's able to maintain its value because the browser submits it with each postback.

To reiterate, here's a rundown of postback that took place in the preceding Try It Out.

+   1. You requested the page in the browser by opening it from VS.
2. The browser gets the page from the server by making a request for it.
3. The ASP.NET run time reads the page from disk, processes it, and sends the resulting HTML to the browser. At this stage, all the controls are set to their default values that were defined in the markup of the page. For example, the Text of the Label control is set to Label.
4. After the page got displayed in the browser, you clicked the Set Date button. This caused a postback to the server.
5. At the server, the page was reconstructed again, similar to the first time it loaded, described in step 3. At this stage, all the controls contain their default values. So, again, the Label control had its Text property set to Label. After the defaults have been set, the time overrides these defaults it finds in View State. However, because this was the first postback and the Label's Text property hadn't changed, its value was not present in View State. So the Text property correctly set the default Label.
6. While still processing the same request, the ASP.NET run time fired in the SetDate_Click. As you have seen, this changed the Text property of the Label control to the current date and time. The ASP.NET run time sees this and stores this new value in View State, and sends it to the browser so it stays available for subsequent postbacks.
7. Next, you entered some text and clicked the Plain Postback button. Just with the other button, this caused a postback to occur. The page was constructed again, and all defaults are set. Again, this means that the Text property of the Label control simply contains the word Label. However, after that, during the same cycle, the ASP.NET run time processes the View State, reconstructing control values it finds in the _VIEWSTATE. In this, it found the Text property with the current date and time, and assigned it to the Label control. Because the Plain Postback button doesn't change the Text of the Label anymore, the Text property doesn't: it contains the date and time from the previous postback. The Text property of the TextBox control is set using the value submitted to the server; that is, the control does not use View State to maintain its value. At end, the entire page is sent to the browser, where the label correctly displays its value.
8. Finally, you turned off the ViewState for the Label and TextBox controls by setting EnableViewState=False. With this turning off, the ASP.NET run time doesn't track the Label anymore. So when you click the Plain Postback button, the ASP.NET run time doesn't find any information for the label in View State, which results in the label displaying its own default text: the word Label.

## Not All Controls Rely on View State

You have to understand that not all controls rely on View State all the time. A number of controls are able to maintain some of their own state, as you saw with the TextBox control, CheckBox, RadioButton, and DropDownList. These include, among others, are able to maintain their values because they are rendered as HTML form controls in the browser. For example, a TextBox server control ends up in this browser:

```
<input name="TextBox1" type="text" value="Initial Text" id="TextBox1" />
```

When a page with a TextBox in it is posted, the server sends the value of the control back to the server. The ASP.NET run time can then simply look up to populate the text box again, instead of getting the value from View State. This is more efficient than storing the value in View State too. If that were the case, the value would get sent to the server twice: once in the text box and once in View State. Especially with large values, this could quickly
