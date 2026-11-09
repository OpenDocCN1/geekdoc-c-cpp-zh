```
</Grid>
</UserControl>
```

In Listing 11.9, a **RichTextBox** control is added to the application. This control contains the formatted text, an image, and a hyperlink. The **Run** element is used to format the small pieces of text. To add an **Image** control to the **RichTextBox** control, the **Image** element is placed within the **InlineUIContainer** element. You can set the **Source** attribute of the **Image** element to the reference of any image you want to add in the application. In this case, we have added the reference of **SL4.png** image.

+   13. Press the **F5** key to run the Web site. The output appears, as shown in Fig.ASP-11.31:

![](bbox=[0.33, 0.27, 0.7, 0.45])

Fig.ASP-11.31

# **Using the WebBrowser Control**

The **WebBrowser** control allows you to create your own Silverlight browser using which you can host the HTML-based content. The **WebBrowser** control provides you two methods, **Navigate()** and **NavigateToString()**, which you can use to navigate to different URLs. The **Navigate()** method takes a URI as a string parameter and redirects you to that URI. The **NavigateToString()** method takes a string parameter representing the HTML content. If you use the **NavigateToString()** method with your **WebBrowser** control, it displays the HTML content specified in the string parameter.

Let's understand the use of WebBrowser control by using it in an application. Perform the following steps to create an application showing the implementation of the **WebBrowser** control:

+   1. *Open* **Microsoft Visual Studio 2010** and *select* **File**➔**New**➔**Project**. The New Project dialog box appears.
+   2. *Select* **Visual C#**➔**Silverlight** from the Installed Templates pane in the New Project dialog box.
+   3. *Select* **Silverlight Application** from the middle pane.
+   4. *Specify* the name of the application as **MyWebBrowser** (also available on CD) in the **Name** text box and the appropriate location in the **Location** combo box.
+   5. *Click* the **OK** button.
+      The **New Silverlight Application** dialog box appears.
+   6. *Select* the Host the Silverlight application in a new Web site check box.
+   7. *Select* the **ASP.NET Web Application Project** option from the **New Web project type** drop down box.
+   8. *Select* **Silverlight 4** from the **Silverlight Version** drop down box.
+   9. *Select* the **Enable WCR RIA Services** check box.
+   10. *Click* the **OK** button.
+       The **MyWebBrowser** application is created.