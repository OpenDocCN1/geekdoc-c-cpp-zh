
2. Select the ASP.NET Web Site template from the middle pane. Select FTP from the Web location drop-down list, and then type the path in the Location box where you want to create the Web site or select the location by clicking the Browse button. The Choose Location dialog box appears, as shown in Figure 13.23:

![](img/e073a4882197be4ab61103cbe0bcb394_680_0.png)

**Figure 13.23:** The Choose Location Dialog Box with the FTP Site Option Selected

3. Click the FTP Site tab. Now enter the server name, the port number and the directory, as shown in Figure 13.23 and click the Open button to return to the New Web Site dialog box.

4. Select the language as Visual C# and click the OK button to create the FTP-based Web site.

## Using Web Application Project

The Web application project type is an alternative to the Web site project. It uses a build model that creates a single assembly for the whole project. Let’s learn how to create a Web application project. For this perform the following steps to create an application called WebApplicationProject:

1. Click the File→New→Project menu item. The New Project dialog box appears, as shown in Figure 13.24:

![](img/e073a4882197be4ab61103cbe0bcb394_680_1.png)

**Figure 13.24:** The New Project Dialog Box

2. Under Installed Templates pane, expand Visual C#, and then click Web to display the available templates.

3. Select ASP.NET Web Application option in the middle pane. In the Name box, type the name of the new application as WebApplicationProject.

4. In the Location box, type the name of the folder in which you want to store the Web application or click Browse button to select a location. Click the OK button. Visual Studio creates the Web application project in the specified location.

Now, you will see how to set a caption for the title bar of a Web Form.

## Setting the Title Bar Text of a Web Form

You can set title bar text for a Web Form by using the Title property in the HTML’s header. By default, you will see the text, Untitled Page in the title bar of the browser when the Web Form is displayed. You can give the Web Form a title of your choice by using the Title property.

> **NOTE**
> To display a title of the Web page, the Web page must contain a `<head>` element with the `runat="server"` attribute; otherwise, the title will not be displayed.

Let’s use the same application named FileSystemWebsite to display a title for its Default Web page. To do so, add a value to the `<Title>` tag of the Default Web page in the Source view, as shown highlighted in Listing 13.4:

**Listing 13.4:** Setting Title of a Web Form

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Welcome Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>

        </div>
    </form>
</body>
</html>
```

You can now run the application by pressing the F5 key. The result is shown in Figure 13.25:

![](img/e073a4882197be4ab61103cbe0bcb394_681_0.png)

In the next section, you can see how to add a background color to a Web Form.

## Adding a Background Color to a Web Form

.NET allows you to change a Web Form’s background color by using the bgColor attribute of the `<body>` tag. Let’s use the FileSystemWebsite application to learn how to change the background color of the Default Web page. To do so, perform the following steps:

1. Select the Web Form in the Design View. Next, in the Properties window, click the ellipsis button of the BgColor property. The More Colors dialog box appears, as shown in Figure 13.26:

![](img/e073a4882197be4ab61103cbe0bcb394_682_0.png)

**Figure 13.26:** The More Colors Dialog Box

2. Select a color and click the OK button, as shown in Figure 13.26. The selected color is applied on the Default Web page using the highlighted line of code given in Listing 13.5.

**Listing 13.5:** Adding Background Color of a Web Form

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Welcome Page</title>
</head>
<body bgcolor="#99ff66">
<form id="form1" runat="server">
<div>

</div>
</form>
</body>
</html>
```

3. Press F5 key to run the Web site, the output appears by changing the background color of the page, as shown in Figure 13.27:

**Figure 13.27:** The Default Web Page with its Background Color Set

In the next section, you will learn to add a background image to a Web Form.

## Adding a Background Image to a Web Form

You can also add a background image to the Default Web page of an application. We use the FileSystemWebsite application to learn how to add a background image to its Default Web page. To do so, perform the following steps:

1. Add an image to the application. Now in the Design View, select the Web page and in the Properties window, click the ellipsis button of the Background property of the Web page. The Select Project Item dialog box appears, as shown in Figure 13.28:

![](img/e073a4882197be4ab61103cbe0bcb394_683_0.png)

**Figure 13.28:** The Select Project Item Dialog Box

> **NOTE**
> To add an image to the application, just copy the image file, right-click the project name in the Solution Explorer and then select the Paste option from the context menu.

2. Select the image file and click the OK button, as shown in Figure 13.28. The selected background image is added to the Default Web page using the highlighted line of code given in Listing 13.6:

**Listing 13.6:** Adding a Background Image to a Web Form

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Welcome Page</title>
</head>
<body background="penguins.jpg" bgcolor="#99ff66">
<form id="form1" runat="server">
<div>

</div>
</form>
</body>
</html>
```

3. Press F5 key to run the application, the output appears, as shown in Figure 13.29:

![](img/e073a4882197be4ab61103cbe0bcb394_684_0.png)

**Figure 13.29:** The Default Web Page with its Background Image Set

Next you will learn to add different controls to a Web Form.

## Adding Controls to a Web Form

The Web Form remains incomplete if it does not contain any Web controls. Typically, almost all Web Forms have controls attached to it. In this section, you learn how to add controls to a Web Form and explore the various properties of the controls. We take the same example of the FileSystemWebsite application and add controls to its Default Web page. To do so, drag and drop from the Toolbox three Label controls, two TextBox controls, and a Button control on the Default Web page and set their text, as shown in Figure 13.30. When you execute the application by pressing F5 key the output is displayed, as shown in Figure 13.30:

**Figure 13.30:** The Design View of the Default Web Page

## Hiding and Displaying Controls

Let's learn how to hide and display controls on the Web page by using their Visible property. We use the FileSystemWebsite application as an example to hide the label, which is at the bottom of the Default Web page when the Web page loads for the first time. To do so, perform the following steps:

1. Select the Label control at design time and set its Visible property to false in the Properties window.

2. Execute the application by pressing F5 key, the result will be displayed, as shown in Figure 13.31:

**Figure 13.31:** Displaying the Page with the Label Hidden

In Figure 13.30 you can see that the label at the bottom of the Web page is visible but in Figure 13.31, it is hidden. Now, if you want to display the hidden label through a button, double-click the button, for example the Welcome button in the Design view and add the following code to the Click event of the button:

```
protected void Button1_Click(object sender, EventArgs e)
{
    Label3.Visible = true;
```
