Finally, you added the line of code to the handler that sends the message:

```
System.Threading.Sleep(5000);
```

This code halts the execution of the page for 5 seconds (the number you pass to the Sleep method expressed in milliseconds) so you can get a look at the message in the UpdateProgress control. In production, you should remove this line, because it slows down the page considerably adding any value to the page.

In addition to user-triggered page updates as you saw with the Send button, you can also trigger page refreshes programmatically at a specified interval, as discussed in the following section.

> NOTE When you wrap server-side functionality in an UpdatePanel, it may sometimes be hard to see if an error has occurred and what the exact error message is. For example, when sending the e-mail fails, you won't see the real error message because it's hidden in the JavaScript. To make it easier to see the error message when something goes wrong, you can temporarily remove the UpdatePanel from the server-side comments using <% and -- like this:
<asp:UpdatePanel ID="up1" runat="server"><ContentTemplate>
    Existing content goes here
</ContentTemplate></asp:UpdatePanel-->

# The Timer Control

The Timer control that you find in the AJAX Extensions of the Toolbox is great for executing server-side code on a repetitive basis. For example, you can use it to update the contents of an UpdatePanel every 5 seconds. The contents of this UpdatePanel could come from a variety of sources, such as a database with the latest forum posts or news items on a news site, an XML file with information to rotate advertisements in the browser, stock quotes from a web service, and more.

The Timer control is pretty simple to use. At a specified interval, the control fires its Tick event. Inside an event handler for this you can execute any code you see. The following code snippet shows the markup for a simple UpdatePanel and a Timer control that you can place inside a content page based on your master page (because the master page already contains the required ScriptManager):

```
<asp:UpdatePanel ID="UpdatePanel" runat="server">
<ContentTemplate>
<asp:Label ID="Label1" runat="server"></asp:Label>
<asp:Timer ID="Timer1" runat="server" Interval="5000" OnTick="Timer1_Tick" />
</ContentTemplate>
</asp:UpdatePanel>
```