

of the page information to another language. Of course, if you actually performed a currency conversion and showed the appropriate euro value along with the culture specification of the currency, that makes sense and is the best solution.

Therefore, if you are using an automatic culture setting on your ASP.NET page and you are not converting the currency, you should perform something similar to the following code for currency values:

```
Dim myNumber As Double = 5123456.00
Dim usCurr As CultureInfo = New CultureInfo("en-US")
Response.Write(myNumber.ToString("c", usCurr))
```

## Understanding Differences in Sorting

You have learned to translate textual values and alter the construction of the numbers, date/time values, currencies, and more when you are globalizing an application. You should also take care when applying culture settings to some of the programmatic behaviors that you establish for values in your applications. One operation that can change based upon the culture setting applied is how .NET sorts strings. You might think that all cultures sort strings in the same way (and generally they do), but sometimes differences exist. For example, the following shows a sorting operation occurring in the en-US culture:

```
Imports System.Collections.Generic

Private Sub Sorting()
    Thread.CurrentThread.CurrentCulture = New CultureInfo("en-US")
    'Thread.CurrentThread.CurrentCulture = New CultureInfo("fi-FI")

    Dim myList As List(Of String) = New List(Of String)

    myList.Add("Washington D.C.")
    myList.Add("Helsinki")
    myList.Add("Moscow")
    myList.Add("Warsaw")
    myList.Add("Vienna")
    myList.Add("Tokyo")

    myList.Sort()

    For Each item As String In myList
        TextBox1.Text += item.ToString() & Environment.NewLine
    Next
End Sub
```

Code snippet from Form1.vb

For this example to work, you have to reference the System.Collections and the System.Collections.Generic namespaces because this example makes use of the List(Of String) object.

In this example, a generic list of capitals from various countries of the world is created in random order. Then the Sort method of the generic List(Of String) object is invoked. This sorting operation sorts the strings according to how sorting is done for the defined culture in which the application thread is running. The preceding code shows the sorting as it is done for the en-US culture. The result of this operation when used within the ProVB2010_Localization form is shown in Figure 27-9.

This is pretty much what you would expect. Now, however, change the previous example so that the culture is set to the Finnish culture. Do this by uncommenting the second line of the Sub Sorting and commenting out the first line of the Sub Sorting which sets the “en-US” culture settings, in the preceding snippet.

If you run the same bit of code under the Finnish culture setting, you get the results presented in Figure 27-10.

![](img/d99870e80390742f93963da7be0b2e61_918_0.png)

# FIGURE 27-9

![](img/d99870e80390742f93963da7be0b2e61_918_1.png)

# FIGURE 27-10

Comparing the Finnish culture sorting shown in Figure 27-10 and the U.S. English culture sorting done in Figure 27-9, you can see that the city of Vienna is in a different place in the Finnish version. This is because in the Finnish language, there is no difference between the letter V and the letter W. Therefore, if you are sorting using the Finnish culture setting, Vi comes after Wa, and thus, Vienna appears last in the list of strings in the sorting operation.

## ASP.NET RESOURCE FILES

When you work with ASP.NET, resources are handled by resource files. A resource file is an XML-based file that has a .resx extension. You can have Visual Studio help you construct this file. Resource files provide a set of items that are utilized by a specified culture. In your ASP.NET applications, you store resource files as either local resources or global resources. The following sections describe how to use each type of resource.

## Making Use of Local Resources

You might be surprised how easily you can build an ASP.NET page so that it can be localized into other languages. In fact, the only thing you need to do is build the ASP.NET page as you normally would and then

use some built-in capabilities from Visual Studio to convert the page to a format that enables you to plug in other languages easily.

To see this in action, build a simple ASP.NET website called ProVB_Localization and open the Default.aspx page as presented here. Note that we have added a few simple controls to replace the default labels generated with a new page. This page will be referred to later in the chapter as the “ASP.NET page code block.” Keep in mind that the downloaded code will not match this initial code snippet as this chapter modifies this code to support multiple languages.

```
<%@ Page Title="Home Page" Language="VB" MasterPageFile="~/Site.Master" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">

<div>
<asp:Label ID="Label1" runat="server"
Text="What is your name?"></asp:Label><br />
<br />
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>&nbsp;
<asp:Button ID="Button1" runat="server" Text="Submit Name" /><br />
<br />
<asp:Label ID="Label2" runat="server"></asp:Label>
</div>

</asp:Content>
```

Code snippet from ProVB_Localization\Default.aspx

As you can see, there is not much to this page. It is composed of a couple of Label controls, as well as TextBox and Button controls. Update the click event handler for Button1 to set the Label2.Text property text to the TextBox1.Text property value. This way, when users enter their name into the text box, the Label2 server control is populated with the inputted name.

The next step is what makes Visual Studio so great. To change the construction of this page so that it can be localized easily from resource files, open the page in Visual Studio and ensure that you are in Design view. Next, using the Visual Studio menu, select Tools ➔ Generate Local Resource. Note that you can select this tool only when you are in the Design view of your page.

Selecting Generate Local Resource from the Tools menu causes Visual Studio to create an App_LocalResources folder in your project if you don’t have one already. A .resx file based upon this ASP.NET page is then placed in the folder. For instance, if you are working with the Default.aspx page, then the resource file is named Default.aspx.resx (see Figure 27-11).

Right-click on the .resx file, select View Code. If View Code isn’t present on your default menu, select Open With; you’ll get a dialog with a list of editor options. From the Open With dialog, select the XML (Text) Editor as the program to open this file using the OK button. After doing this, you should find the View Code option on the context menu for this file. When the .resx file opens, you’ll notice that the .resx file is nothing more than an XML file with an associated schema at the beginning of the document. The resource file that is generated for you takes every possible property of every translatable control on the page and gives each item a key value that can be referenced in your ASP.NET page. Looking at the page’s code, note that all the text values you placed in the page have been retained, but

![](img/d99870e80390742f93963da7be0b2e61_919_0.png)

FIGURE 27-11

they have also been placed inside the resource file. Visual Studio changed the code of the `Default.aspx` page as shown in the following code block:

```
```aspx
<%@ Page Title="Home Page" Language="VB" MasterPageFile="~/Site.Master"
    AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default"
    culture="auto" meta:resourcekey="PageResource1" uiculture="auto" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:Label ID="Label1" runat="server"
            Text="What is your name?" meta:resourcekey="Label1Resource1"></asp:Label>
        <br /> <br />
        <asp:TextBox ID="TextBox1" runat="server"
            meta:resourcekey="TextBox1Resource1"></asp:TextBox>&nbsp;
        <asp:Button ID="Button1" runat="server" Text="Submit Name"
            meta:resourcekey="Button1Resource1" /> <br />
        <br />
        <asp:Label ID="Label2" runat="server" meta:resourcekey="Label2Resource1"></asp:Label>
    </div>

</asp:Content>
```
```

*Code snippet from ProVB_Localization\Default.aspx*

From this bit of code, you can see that the Culture and UICulture attributes have been added to the `@Page` directive with a value of auto, thus, enabling this application to be localized. In addition, the attribute `meta:resourcekey` has been added to each of the controls, along with an associated value. This is the key from the `.resx` file that was created on your behalf. Double-clicking on the `Default.aspx.resx` file opens the resource file in the Resource Editor, shown in Figure 27-12, built into Visual Studio. Keep in mind the code download will have additional settings not shown if you are working along with the chapter.

![](img/d99870e80390742f93963da7be0b2e61_920_0.png)

