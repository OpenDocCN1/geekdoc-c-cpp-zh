# Launching Internet Explorer from Your Windows Application

Sometimes, the goal is not to host a browser inside the application but to allow users to find the website in a typical Web browser. For an example of this task, add a LinkLabel control (named JumpLink) to the MyBrowser form. For instance, you can have a form that has a LinkLabel control on it that simply states “Visit your company website!”

Once this control is in place, use the following code to launch the company’s website in an independent browser, as opposed to directly in the form of your application:

```
Public Class MainForm
    Private Sub JumpLink_LinkClicked(ByVal sender As System.Object, _
            ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) Handles _
            LinkLabel1.LinkClicked
        Dim wb As New WebBrowser
        wb.Navigate("http://www.wrox.com", True)
    End Sub
End Class
```

> Code snippet from MyBrowser

In this example, when the LinkLabel control is clicked by the user, a new instance of the WebBrowser class is created. Then, using the WebBrowser control’s Navigate method, the code specifies the location of the Web page, as well as a Boolean value that specifies whether this endpoint should be opened within the Windows Form application (a False value) or from within an independent browser (a True value). By default, this is set to False. With the preceding construct, when the user clicks the link found in the Windows application, a browser instance is instantiated and the Wrox website is immediately launched.

# Updating URLs and Page Titles

Note that when working with the MyBrowser example in which the WebBrowser control is directly in the form, when you click the links, the text in the AddressField control is not updated. You can fix this by listening for events coming off the WebBrowser control and adding handlers to the control.

It is easy to update the form’s title with the HTML page’s title. Create a DocumentTitleChanged event and update the form’s Text property:

```
Private Sub TheBrowser_DocumentTitleChanged(ByVal sender As Object,
    ByVal e As System.EventArgs) Handles TheBrowser.DocumentTitleChanged
        Me.Text = TheBrowser.DocumentTitle.ToString()
End Sub
```

> Code snippet from MyBrowser

In this case, when the WebBrowser control notices that the page title has changed (due to changing the page viewed), the DocumentTitleChanged event will fire. In this case, you change the form’s Text property (its title) to the title of the page being viewed using the DocumentTitle property of the WebBrowser control.

Next, update the text string that appears in the form’s text box, based on the complete URL of the page being viewed. To do this, you can use the WebBrowser control’s Navigated event:

```
Private Sub TheBrowser_Navigated(ByVal sender As Object, _
    ByVal e As System.Windows.Forms.WebBrowserNavigatedEventArgs) Handles _
    TheBrowser.Navigated
        AddressField.Text = TheBrowser.Url.ToString()
End Sub
```

> Code snippet from MyBrowser

In this case, when the requested page is finished being downloaded in the WebBrowser control, the Navigated event is fired. You simply update the Text value of the AddressField control to be the URL of the page. This