# Chapter 13: Introducing ASP.NET 4.0 and Web Forms

```
Text="Click Me" OnClientClick = "button1_onclick()"/>
<asp:TextBox ID="TextBox1" runat="server"
style="top: 156px; left: 364px; position: absolute;
height: 22px; width: 196px"/></asp:TextBox>
</form>
</body>
</html>
```

In the code, the OnClientClick event is always executed first since it happens on the client-side, when you view the Web page in your browser, whereas the OnClick event is executed on the server where the page arrives after a postback. Clicking the button, runs the code in the JavaScript button1_onclick event handler.

+   4. Add this line of JavaScript in the Source view of the page to display the text, Handling client events, into TextBox1, using the following code:

```
function button1_onclick()
{
document.getElementById("TextBox1").value = "Handling client events";
}
```

That is all it takes—except here, we are writing code in JavaScript, not in Visual C#, because we want this code to execute in the client (that is, the browser).

+   5. Press F5 key to execute the application and the result is displayed, as shown in Figure 13.46:

![](bbox=[0.18, 0.385, 0.85, 0.635])

# Figure 13.46: Handling the Client Events

+   6. Click the Click Me button, the text Handling Client Events appears in text box—all without triggering a postback to the server. Our code will usually use a postback to the server, and use Visual C# instead of JavaScript, but it is worth knowing that you can also handle client events in this way.

Next, you will see how to handle the navigation of multiple pages in a Web site. In addition, you will also learn to implement cross-page posting in your application.

# Web Forms Navigation and Cross-Page Posting

In ASP.NET, you can create Web sites that are dynamic in nature. When a user requests for a Web page (.aspx file), the Web page performs the tasks that the Web site requires, such as calculating values, reading or writing database information, or calling other programs on the Web server. The Web page dynamically generates HTML or any other markup language as output and sends it to the browser.

ASP.NET pages run as code on the Web server. Therefore, the pages are configured so that they can be submitted to the server when a user clicks a button, or selects checkboxes, or interacts with other controls in the Web page to process the page on the Web server. Every time, the Web page submits data back to itself so that it can run its server code again to produce the new version of itself for the user. The process in which a Web page sends data back to the same page on the server is known as postback of a Web page.