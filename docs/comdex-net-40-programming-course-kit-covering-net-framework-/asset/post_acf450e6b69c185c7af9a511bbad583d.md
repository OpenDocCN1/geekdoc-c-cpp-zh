
Add the code, shown in Listing 8.14, in SkinFile.skin file:

**Listing 8.14:** Showing the Code for the **SkinFile.skin** File

```aspx
<asp:Table runat="server" Width="100px" Font-Bold="False" Font-Size="Medium"
    ForeColor="Green" />

<asp:Button runat="server" ForeColor="Blue" BackColor="Gray"/>

<asp:TextBox runat="server" Font-Bold="False" Font-Size="Medium" ForeColor="Red"
    BackColor="Silver" Font-Style="True"/>
```

In Listing 8.14, we have specified the style of controls.

- 11. *Right-click* the project name in **Solution Explorer** and select **Add New Item** from the context menu. The **Add New Item** dialog box opens.
- 12. *Select* **Web Form** from the middle pane of the **Add New Item** dialog box.
- 13. *Click* the **Add** button to add the **Default.aspx** page to your project.
- 14. *Replace* the code of the **Default.aspx** page with the code shown in Listing 8.15:

**Listing 8.15:** Showing the Code for the **Default.aspx** Page of the **StyleSheetThemesAttribute** Application

```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
    Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" BackColor="#666633"
                ForeColor="Yellow"
                Text="Label" Width="200px"></asp:Label> <br />
            <br />
            <asp:Label ID="Label2" runat="server" Text="Enter Name"></asp:Label>
            &nbsp;&nbsp;
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <br />
            <br />

            <asp:Label ID="Label3" runat="server" Text="Address"></asp:Label>
            &nbsp;&nbsp;
            <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
            <br />
            <br />
                &nbsp;&nbsp;&nbsp;&nbsp;
            <asp:Button ID="Button1" runat="server" Text="Submit" />
        </div>
    </form>
</body>
</html>
```

The design of your page is shown in Fig.ASP-8.24:

![](img/9862a98a1a2d3bb14334137965a1ec60_656_0.png)

Fig.ASP-8.24

- 15. **Double-click** the **Submit** button and add the code, shown in Listing 8.16, in its click event:

**Listing 8.16:** Showing the Code for the Click Event of **Submit** button

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    Label1.Text = "Welcome "+TextBox1.Text;
}
```

Listing 8.16 concatenates the string **Welcome** with **TextBox1** control value and sets the **Text** property of the Label1 control to the concatenated value. For example, when user enters **Kogent** in the **TextBox1** control, then the value of **Text** property of **Label1** control will be **Welcome Kogent**.

- 16. **Add** the **StylesheetTheme** attribute in the **@ Page** directive to apply the styles defined in the SkinFile.skin file to the controls, as shown in the following code snippet:

```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
    Inherits="_Default" StylesheetTheme="Theme1" %>
```

It is important to note that the **StylesheetTheme** attribute enables you to view the applied theme at design time; while the Theme attribute enables you to view the applied theme only at runtime.

- 17. **Select** the **Design** tab to view the design of **Default.aspx** page, as shown in Fig.ASP-8.25:

![](img/9862a98a1a2d3bb14334137965a1ec60_656_1.png)

Fig.ASP-8.25

Now, you can understand the difference between the **Theme** attribute and **StylesheetTheme** attribute. As stated earlier that the **StylesheetTheme** attribute does not override the local controls properties or attributes. Therefore, in Fig.ASP-8.25, the style of Label1 control is not changed.

- 18. Press the F5 key to run the application (Fig.ASP-8.26).
- 19. Enter your name and address in the respective TextBox controls (Fig.ASP-8.26).
- 20. Click the Submit button to set the Text property of the Label1 control (Fig.ASP-8.26).

The Text property of the Label1 control is set to Welcome Kogent (Fig.ASP-8.27).

![](img/9862a98a1a2d3bb14334137965a1ec60_657_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_657_1.png)

With this, we come to the end of the chapter. Now, let’s summarize the main points of this chapter.

### Summary

In this chapter, you have learned about master pages, including simple and nested master pages. Next, you have learned about themes, which includes how to create themes and apply them on controls at runtime. Finally, you have learned about the StylesheetTheme attribute.

In the next chapter, you learn about caching in ASP.NET 4.0.

CHAPTER

## Caching in ASP.NET 4.0

![](img/9862a98a1a2d3bb14334137965a1ec60_658_0.png)

In this Chapter:

- Caching in ASP.NET
- Introducing the Cache Class
- Describing Output Caching
- Implementing Output Caching
- Describing Partial-Page Output Caching
- Understanding the Disk Output Cache
- Describing Post-Cache Substitution and Substitution Control
- Data Caching
- Implementing Data Caching
- Explaining Cache Dependencies

Caching is a technique that is used to temporarily store the frequently accessed Web pages (or data) in memory. It helps in accessing Web pages faster than accessing them from the original source. For example, when you access a Web page for the first time, it takes some time to get loaded. However, subsequent visits to that Web page become faster because the Web page has been cached on your computer. You may cache a whole Web page, parts of a Web page, or application data, according to your requirements. There may be certain items on a Web site that you want to cache after a specific time interval. For example, you are running a news Web site and you want the content on your Web site to be refreshed at regular intervals, say after every half an hour, ten minutes, or even every minute. In this situation, the specified content of the Web site is stored in the cache memory for a particular time, say an hour. Then, after every hour, the cache memory refreshes and retrieves the data from the database or the server.

In this chapter, you learn about caching in ASP.NET. Next, you learn about the Cache class. You also learn about different types of caching, such as output caching, partial-page output caching, disk output caching, and data caching. Further, you learn about post-cache substitution and the Substitution control. In the end, you learn about cache dependencies.

Let’s start by learning about caching.

### Caching in ASP.NET

Caching can be used to improve the processing time and the performance of a Web application as it allows you to access data from the cache stored in your local computer, which is faster than retrieving the data from the database on each request. Therefore, caching not only reduces the processing time of your Web application but also reduces the network traffic.

.NET Framework provides you a number of classes, such as the **Cache** class, which you can use to cache the data in your Web applications. With the release of .NET Framework 4.0, the caching feature has also been extended.

In ASP.NET 4.0, the following new caching features have been introduced:

- **Extensible Output Caching:** Enables you to configure more than one custom output-cache provider. Output-cache providers allow you to store cached data in various storage devices, such as disks. Output caching, first introduced with ASP.NET 1.0 that enables you to store the page output and Hypertext Transfer Protocol (HTTP) responses in an in-memory cache, which stores the cache data in Random Access Memory (RAM) of the computer. It helps in generating the content faster by not regenerating the output from scratch. However, in ASP.NET 4.0, the output caching feature has been extended. A new **System.Web.Caching.OutputCacheProvider** class has been introduced to enable you to create a custom output-cache provider, which can then be registered within the **web.config** file of an application by using the new **<providers>** subsection of the **<outputCache>** element.
- **Object Caching:** Helps in making caching available for all applications by introducing the new **System.Runtime.Caching.dll** assembly, which contains the new **System.Runtime.Caching** namespace. There are the following two sets of classes in the **System.Runtime.Caching** namespace:
  - **Abstract types:** Provide the base for implementing custom cache.
  - The **System.Runtime.Caching.MemoryCache** class: Allows you to implement caching even in the applications that are not the ASP.NET applications.

Now, let’s learn about the Cache class that provides various methods and properties to implement caching in a Web application.

### Introducing the Cache Class

In ASP.NET, the System.Web.Caching.Cache class is used to implement caching for a Web application.

It is important to note that the System.Web.Caching.Cache class cannot be inherited. Some noteworthy properties of the Cache class are listed in Table 9.1:
