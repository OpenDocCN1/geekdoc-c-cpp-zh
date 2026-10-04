
# USING ASP.NET AJAX IN YOUR PROJECTS

ASP.NET AJAX is fully integrated in ASP.NET and VS, which means you can start it right away. Each new ASP.NET 4.5.1 web project you create in VS is already Ajax-enabled. In addition, the Toolbox contains an AJAX Extensions gallery with a number of Ajax-related controls that you can use in your pages. Visual Studio has great support for ASP.NET AJAX, giving you IntelliSense for the controls as well as for the client-side JavaScript you'll write to interact with the client page and code running on the server.

# Creating Flicker-free Pages

To avoid full postbacks in your ASPX pages you can use only part of the page, use the UpdatePanel control. For this to operate correctly, you also need a ScriptManager control. If you're going to use functionality in many of your ASPX pages, you can place the ScriptManager in the master page, so it's available in all pages that are managed by this master. You have only one ScriptManager per page, so if you add one to master page, you can't add another to a content page. To access a ScriptManager control that is defined in a master page from a content page, you can use the ScriptManagerProxy control as explained. You'll find these other Ajax-related controls in the AJAX Extensions gallery of the Toolbox, shown in Figure 10-2.

![](img/9e033e3b9560597824f8b22941d6d8bb_377_0.png)

The following two sections introduce you to the UpdatePanel and ScriptManager controls. After the introduction you will learn how to use these controls in the pages of your Planet Wrox website. Later sections introduce you to the UpdateProgress, Timer, and ScriptManager Proxy controls.

# The UpdatePanel Control

The UpdatePanel control is a key component in creating flicker-free pages. In its most basic application, you wrap the control over content you want to update, add a ScriptManager to the page, and when one of the controls within the UpdatePanel causes a postback to the server, only the content within that UpdatePanel is refreshed.

To see what problems the UpdatePanel control solves and how it behaves in a client page, the following Try It Out shows a simple example that uses the panel to avoid page flicker during postbacks.

# TRY IT OUT Adding an UpdatePanel to a Page

In this exercise, you add a Label and a button to a page. When you click the button in the browser, the Text property of the Label is updated with the current date and time at the server. To avoid the page flicker typically associated with postbacks, you then wrap the controls in an UpdatePanel to see how that affects the behavior.

1. Open the Planet Wrox website in Visual Studio.
2. In the Demos folder, create a new Web Form UpdatePanel.aspx using your custom template. Give the page a Title of UpdatePanel Demo.

Switch the new page into Design view and drag a Label and a Button control from the Toolbox into the cpMainContent placeholder. If the ContentPlaceHolder suddenly gets small as the Label, simply drop the Button on top of the Label. The Button is then placed before the Label if you now drag the Label on top of the Button again, the two changes place.

Use the Properties Grid to clear the Text property of the Label control. To do this, right-click the Text property label in the Properties Grid and choose Reset.

Double-click the grid and read-only area of the page in Design view to set up a handler for its Load event and add the code you added for:

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Label.Text = System.DateTime.Now.ToString()
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs args)
{
    Label.Text = System.DateTime.Now.ToString();
}
```

Save all your changes and press Ctrl+F5 to open the page in your browser.

The Label displays the date and time. Click the Button control a few times. Note that each time you click the button, the page flickers and is redrawing, displaying the updated date and time. Take a look at the HTML that is used by the browser (right-click the button in the browser and choose View Source or Page Source). Notice how the page contains a <span> element with the date that was sent from the server.

Close your browser, go back into VS, and switch the UpdatePanel.aspx page to Markup View. Make some room here before the Label control, and then updatepanel and press Tab. VS inserts the code for an UpdatePanel and a <ContentTemplate> for.

Next, cut both the <ContentTemplate> and </UpdatePanel> tags and place them below the control you created in step 3. You should end up with this markup:

```
<UpdatePanel runat="server">
<ContentTemplate>
  <asp:Label Id="Label1" runat="server"></asp:Label>
  <asp:Button Id="Button1" runat="server" Text="Button" />
</ContentTemplate>
</UpdatePanel runat="server">
```

Right before the opening tag of the UpdatePanel, drag a ScriptManager from the AJAX Extensions category of the Toolbox. Alternatively, press tab by the Tab key to insert the ScriptManager using a code snippet. The code should look similar to this (your ScriptManager may have the ID attribute and use a self-closing element when you use a code snippet:

```
<asp:Content Id="Content" ContentPlaceholderID="cpMainContent" runat="server">
<asp:ScriptManager Id="ScriptManager1" runat="server"></asp:ScriptManager>
<UpdatePanel runat="server">
```

10. Save your changes and request the page in the browser. Click the button a few times to update the label with the current date and time. Note that there is no page flicker now, and only the label is updated on the page. If you look at source in the browser again, you see the <span> element that contains the date and time of first request. The updates that were added by clicking the button are not part of the HTML source because they have been added dynamically by the ASP.NET AJAX Framework to the browser's HTML.

# How It Works

By wrapping the content in an UpdatePanel you define a region on the page that you want to refresh without affecting the entire page. Example, the Button control inside the UpdatePanel causes a postback and then a refresh of just the region in which the control is defined. Rather than replacing the entire page, only the part of the page that is wrapped in the UpdatePanel is refreshed, a flicker-free load of page.

If you analyze the data from the server to the browser (using a network analysis tool like Fiddler which you can download), you would only see a limited amount of data. Rather than the full page around 12KB, the following data is sent:

```
1|#|23|UpdatePanel|cpMainContent
<span id="cpMainContent_Label">12/21/2013 11:59:06</span>
<input type="submit" name="Button" value="Button"
style="background-color:#F7A0A;" />
id="cpMainContent_Button" class="MyButton"
0|hiddenField|EVENTARGUMENT|0|hiddenField|EVENTARGUMENT|0|LASTPOSTBACK|1624|hiddenField|VIEWSTATE|1atynisXn66ScriptPath|ScriptSource.axd?zrvkiHT72ZFNkyU0M1Z5DO77JbsB
4kORh1k2Vyds8RAUqqe5t=5192
```

Note that is a big piece of content including such the ViewState of the page (represented by the three dots). If you look at this, you recommend the HTML for the updated label and the Button; the two controls that have been defined using the <ContentTemplate> of the UpdatePanel control. The remaining text is used by the ASP.NET AJAX Framework to maintain state (using the __VIEWSTATE field) and where to place the response in the page. When a lot of data sent down goes, it's far less than the original full page. This results in a faster and better user experience.

Besides the aforementioned Fiddler tool we advise you to look at the Microsoft Explorer Developer Tool. It ships with Internet Explorer 8 and later can be opened (and closed) by pressing F12. For Windows 8 you need to use the desktop version of Internet Explorer.

Another great tool for debugging is debugger, once you activate it with the Firefox browser. You can get the tool at http://getdebugger.com. Chrome has a tab that you can open by clicking the menu or wrench icon when choosing Tools 🔧 Developers.
