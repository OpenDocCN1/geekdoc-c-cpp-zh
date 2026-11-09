
```xml
<sdk:TreeViewItem Header="Ruby" FontFamily="Courier New"
                 FontSize="10" Foreground="MidnightBlue">
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</sdk:TreeViewItem>
</Grid>
</UserControl>
```

12. Press **F5** to run the **SilverlightTreeView** application. The output appears (Fig. ASP-11.28).

13. Click the triangular glyph on the left side of the root node, Programming Languages, to expand it and view its child nodes. The output after expanding the root node appears (Fig. ASP-11.29).

![](img/9862a98a1a2d3bb14334137965a1ec60_722_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_722_1.png)

As you can see in Fig. ASP-11.29, the root node of the TreeView control displays its child nodes. You can further expand the child nodes to view their child nodes.

## Using the RichTextBox control

The RichTextBox control is one of the new controls in Silverlight 4.0. It is similar to the simple TextBox control that enables you to display the rich content including the formatted text, paragraphs, inline images, and hyperlinks. You can also edit the content of this control dynamically. You can change the font-size, weight, and color of a particular text. To edit the small chunk of text in the RichTextBox control, you can use the Run element, which is derived from the Inline element.

Perform the following steps to use the RichTextBox control in your application:

1. *Open* **Microsoft Visual Studio 2010 IDE** and select **File→New→Project**. The New Project dialog box appears.
2. *Select* **Visual C#→Silverlight** from the **Installed Templates** pane in the New Project dialog box.
3. *Select* **Silverlight Application** from the middle pane.
4. *Specify* the name of the application as **RichTextBoxExample** (also available on CD) in the Name text box and the appropriate location in the Location combo box.
5. *Click* the **OK** button. The **New Silverlight Application** dialog box appears.
6. *Select* the **Host the Silverlight application in a new Web site** check box.
7. *Select* the **ASP.NET Web Application Project option** from the **New Web project type** drop down box.
8. *Select* **Silverlight 4** from the **Silverlight Version** drop down box.
9. *Select* the **Enable WCF RIA Services** check box.
10. Click the **OK** button.

    The *RichTextBoxExample* application is created.

11. Drag a **RichTextBox** control from the **Toolbox** and drop it on the **MainPage.xaml** file, as shown in Fig. ASP-11.30:

![](img/9862a98a1a2d3bb14334137965a1ec60_723_0.png)

Fig. ASP-11.30

12. Replace the code of the **MainPage.xaml** file with the code shown in Listing 11.9, to design the UI of your application:

### Listing 11.9: Showing the Code for the **MainPage.xaml** File of the **RichTextBoxExample** Application

```xml
<UserControl x:Class="RichTextBoxExample.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
        <RichTextBox HorizontalAlignment="Center" Margin="10,12,0,0" Name="contentBox"
            VerticalAlignment="Center" Height="257" Width="368" IsReadOnly="True">
            <Paragraph FontFamily="Georgia" FontSize="12" TextAlignment="Justify">
                Hello, this is the example of
                <Run Text="RichTextBox" FontStyle="Italic" FontWeight="ExtraBold"
                    Foreground="Red"/> control in
                <Run Text="Silverlight4.0" FontStyle="Italic" FontWeight="ExtraBold"
                    Foreground="Red"/>
                <InlineUIContainer>
                    <Image Height="143" HorizontalAlignment="Left" Margin="144,50,0,0"
                        Name="image1" Stretch="Uniform" VerticalAlignment="Top" Width="196"
                        Source="/RichTextBoxExample;component/Images/SL4.png"
                        UseLayoutRounding="True" />
                </InlineUIContainer>
                <LineBreak/>
                <Hyperlink NavigateUri="http://msdn.microsoft.com/en-us/library/ee681613(v=VS.95).aspx" MouseOverForeground="#FFED2600">
                    Click here to read more about the RichTextBox
                    control</Hyperlink>
            </Paragraph>
        </RichTextBox>
    </Grid>
</UserControl>
```

In Listing 11.9, a **RichTextBox** control is added to the application. This control contains the formatted text, an image, and a hyperlink. The **Run** element is used to format the small pieces of text. To add an **Image** control to the **RichTextBox** control, the **Image** element is placed within the **InlineUIContainer** element. You can set the **Source** attribute of the **Image** element to the reference of any image you want to add in the application. In this case, we have added the reference of **SL4.png** image.

13. Press the **F5** key to run the Web site. The output appears, as shown in Fig. ASP-11.31:

![](img/9862a98a1a2d3bb14334137965a1ec60_724_0.png)

Fig. ASP-11.31

## Using the WebBrowser Control

The **WebBrowser** control allows you to create your own Silverlight browser using which you can host the HTML-based content. The **WebBrowser** control provides you two methods, **Navigate()** and **NavigateToString()**, which you can use to navigate to different URLs. The **Navigate()** method takes a URI as a string parameter and redirects you to that URI. The **NavigateToString()** method takes a string parameter representing the HTML content. If you use the **NavigateToString()** method with your **WebBrowser** control, it displays the HTML content specified in the string parameter.

Let's understand the use of WebBrowser control by using it in an application. Perform the following steps to create an application showing the implementation of the **WebBrowser** control:

1. *Open* **Microsoft Visual Studio 2010** and *select* **File➔New➔Project**. The New Project dialog box appears.
2. *Select* **Visual C#➔Silverlight** from the Installed Templates pane in the New Project dialog box.
3. *Select* **Silverlight Application** from the middle pane.
4. *Specify* the name of the application as **MyWebBrowser** (also available on CD) in the **Name** text box and the appropriate location in the **Location** combo box.
5. *Click* the **OK** button.

    The **New Silverlight Application** dialog box appears.

6. *Select* the **Host the Silverlight application in a new Web site** check box.
7. *Select* the **ASP.NET Web Application Project** option from the **New Web project type** drop down box.
8. *Select* **Silverlight 4** from the **Silverlight Version** drop down box.
9. *Select* the **Enable WCF RIA Services** check box.
10. *Click* the **OK** button.

    The **MyWebBrowser** application is created.

Before using a **WebBrowser** control in your application, it is important to note that the **WebBrowser** control only works in an **Out-of-Browser** enabled application. Therefore, perform the following steps to enable the **Out-of-Browser** property of the application:

11. *Right-click* the **MyWebBrowser** application in the **Solution Explorer** window and *select* the **Properties** option from the context menu, as shown in Fig. ASP-11.32:

![](img/9862a98a1a2d3bb14334137965a1ec60_725_0.png)

12. *Select* the **Silverlight** tab of the **Properties** page and then select the **Enable running application out of the browser** check box, under the **Silverlight Build** option (Fig. ASP-11.33).

13. *Click* the **Out-of-Browser Settings...** button, as shown in Fig. ASP-11.33:

![](img/9862a98a1a2d3bb14334137965a1ec60_725_1.png)

The **Out-of-Browser Settings** dialog box appears (Fig. ASP-11.34).

14. *Select* the **Require elevated trust when running outside the browser** check box in the **Out-of-Browser Settings** dialog box and *click* the **OK** button, as shown in Fig. ASP-11.34:
