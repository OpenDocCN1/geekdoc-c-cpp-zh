8. Copy the exact same rule into the DarkGrey.css file for the DarkGrey theme.

9. Switch back to the Contact.ascx user control and begin the closing tag of the UpdatePanel at the end of the file, drag an UpdateProgress control from the AJAX Extensions category of the Toolbox. Set its AssociatedUpdatePanelID to UpdatePanel1, the ID of the UpdatePanel defined earlier in the page.

10. Between the <UpdateProgress> tags create a <ProgressTemplate> element, and within this template, create a <div> element with its class attribute set to PWait, the CSS class you created in step 7. Inside the <div> element, some text to inform your users that they should hold on for a while. When you end your code with:

```
</asp:UpdatePanel>
<asp:UpdateProgress Id="UpdateProgress" runat="server"
    AssociatedUpdatePanelID="UpdatePanel1">
  <ProgressTemplate>
    <div class="PWait">
      Wait...
    </div>
  </ProgressTemplate>
</asp:UpdateProgress>
```

11. To emulate a long delay while waiting for the message so you can see the UpdateProgress control, add the following line of code to the Code Behind of control, just after the lines that change the visibility of the controls in the method that ends with the e-mail:

```
VB.NET

Message.Visible = True
FormTable.Visible = False
System.Threading.Sleep(5000)
```

# C#

```
Message.Visible = true;
FormTable.Visible = false;
System.Threading.Sleep(5000);
```

12. Save all your changes and open the Contact.aspx page from the About folder once. Fill in the required details and click the Send button. Shortly after you click the button, you will see the UpdateProgress control appear that displays text and an animated image below the form, in Figure 10-4. Shortly after, the UpdateProgress control and the entire form should disappear and you should be presented with the Message sent.

> COMMON MISTAKES If you don't see the described behavior, your browser may be working with an outdated version of the CSS files. Press Ctrl+F5 and Ctrl+R to get the latest version from the server and try again. Alternatively, you can clear the browser’s cache.