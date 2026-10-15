
In addition, pay attention to neutral culture when working with your applications. In most cases, you are going to build applications with views that are more dependent on a neutral culture than on a specific culture. For instance, if you have a Spanish version of your application, you'll probably make this version available to all Spanish speakers regardless of where they live. In many applications, it won't matter whether the Spanish speaker is from Spain, Mexico, or Argentina. In cases where it does make a difference, use the specific culture settings.

## Looking at Your Thread

When the end user requests an ASP.NET page or runs a Windows Forms dialog, the item is executed on a thread from the thread pool. That thread has a culture associated with it. You can get information about the culture of the thread programmatically and then check for particular details about that culture.

To see an example of working with a thread and reading the culture information of that thread, start with the basic Windows Forms application created in Chapter 1. To reproduce this create a new project called ProVB2010_Localization, and add the appropriate button and text box controls. A copy of the code in this chapter is part of the code download with the name ProVB2010_Localization.

Add a new Sub DisplayCultureInfo and have it called by the Click event handler for the test button on the form. When the TestButton_Click event is fired, the user's culture information is retrieved and displayed in the TextBox control. The code for the new Sub is presented here:

```
Private Sub DisplayCultureInfo()
    Dim ci As New System.Globalization.CultureInfo(
        System.Threading.Thread.CurrentThread.CurrentCulture.ToString())
    TextBox1.Text = "CURRENT CULTURE'S INFO" & Environment.NewLine
    TextBox1.Text += "Name: " & ci.Name & Environment.NewLine
    TextBox1.Text += "Parent Name: " & ci.Parent.Name & Environment.NewLine
    TextBox1.Text += "Display Name: " & ci.DisplayName & Environment.NewLine
    TextBox1.Text += "English Name: " & ci.EnglishName & Environment.NewLine
    TextBox1.Text += "Native Name: " & ci.NativeName & Environment.NewLine
    TextBox1.Text += "Three Letter ISO Name: " &
        ci.ThreeLetterISOLanguageName & Environment.NewLine
    TextBox1.Text += "Calendar Type: " & ci.Calendar.ToString() & Environment.NewLine
End Sub
```

Code snippet from Form1.vb

This simple form creates a CultureInfo object from the System.Globalization namespace and assigns the culture from the current thread that is running using the System.Threading.Thread.CurrentThread.CurrentCulture.ToString call. Once the CultureInfo object is populated with the end user's culture, details about that culture can be retrieved using a number of available properties that the CultureInfo object offers. Example results of running the form are shown in Figure 27-2.

Note that in the code download there is an additional button on the form based on additional changes that are made to this sample project.

The CultureInfo object contains a number of properties that provide you with specific culture

![](img/d99870e80390742f93963da7be0b2e61_909_0.png)

FIGURE 27-2

information. The items displayed are only a small sampling of what is available from this object. From this figure, you can see that the en-US culture is the default setting in which the thread executes. In addition to this, you can use the CultureInfo object to get at a lot of other descriptive information about the culture. You can always change a thread’s culture on the overloads provided via a new instantiation of the CultureInfo object, as shown here:

```
```vb
Private Sub DisplayCultureInfo()
    System.Threading.Thread.CurrentThread.CurrentCulture =
        New Globalization.CultureInfo("th-TH")
    Dim ci As Globalization.CultureInfo =
        System.Threading.Thread.CurrentThread.CurrentCulture

    ' Dim ci As New System.Globalization.CultureInfo(
    '     System.Threading.Thread.CurrentThread.CurrentCulture.ToString())
    TextBox1.Text = "CURRENT CULTURE'S INFO" & Environment.NewLine
    TextBox1.Text += "Name: " & ci.Name & Environment.NewLine
    TextBox1.Text += "Parent Name: " & ci.Parent.Name & Environment.NewLine
    TextBox1.Text += "Display Name: " & ci.DisplayName & Environment.NewLine
    TextBox1.Text += "English Name: " & ci.EnglishName & Environment.NewLine
    TextBox1.Text += "Native Name: " & ci.NativeName & Environment.NewLine
    TextBox1.Text += "Three Letter ISO Name: " &
        ci.ThreeLetterISOLanguageName & Environment.NewLine
    TextBox1.Text += "Calendar Type: " & ci.Calendar.ToString() & Environment.NewLine
End Sub
```
```

![](img/d99870e80390742f93963da7be0b2e61_910_0.png)

In this example, only a couple of lines of code are changed to assign a new instance of the CultureInfo object to the CurrentCulture property of the thread being executed by the application. The culture setting enables the CultureInfo object to define the culture you want to utilize. In this case, the Thai language of Thailand is assigned. The results produced in the TextBox control are illustrated in Figure 27-3.

From this figure, you can see that the .NET Framework provides the native name of the language used even if it is not a Latin-based letter style. In this case, the results are presented for the Thai language in Thailand, including some of the properties associated with this culture (such as an entirely different calendar than the one used in Western Europe and the United States).

## Declaring Culture Globally in ASP.NET

ASP.NET enables you to easily define the culture that is used either by your entire ASP.NET application or by a specific page within your Web application, using what are termed *server-side culture declarations*. You can specify the culture for any of your ASP.NET applications by means of the appropriate configuration files. To demonstrate this, close the ProVB2010_Localization application you started with and create a new ASP.NET website called ProVB_Russian. Alternatively, you can open this download folder as a website in Visual Studio 2010. On the default.aspx page add a new Calendar control from the toolbox, following the text: Welcome to ASP.NET!

To change the default language used by this control you can specify culture settings in the web.config file of the application itself, as illustrated here:

```
<configuration>
  <system.web>
    <globalization culture="ru-RU" uiCulture="ru-RU" />
  </system.web>
</configuration>
```

Code snippet from ProVB_Russian\web.config

Only the <globalization> line will need to be added to your default web.config file; it should also be noted that based on the page specific settings described below, this line has been commented out in the code download.

Note the two attributes represented: culture and uiCulture. The culture attribute enables you to define the culture to use for processing incoming requests, whereas the uiCulture attribute enables you to define the default culture needed to process any resource files in the application (use of these attributes is covered later in the chapter).

Note that one additional option you have when specifying a culture on the server is to define this culture in the root web.config file for the server. Thus, if you are setting up a web server that will be used with only a single culture, you can specify that culture at the server level, instead of needing to specify it as part of the settings for each application running on the server. This can be useful if you are installing Web applications created outside of your native culture, but where you want date, currency, sorting, and similar formats to default appropriately.

In the preceding snippet, the culture established for this ASP.NET application is the Russian language in the country of Russia. In addition to setting the culture at either the server-wide or the application-wide level, another option is to set the culture at the page level, as shown here:

```
<%@ Page Title="Home Page" Language="VB" MasterPageFile="~/Site.Master" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" UICulture="ru-RU" Culture="ru-RU" %>
```

Code snippet from ProVB_Russian\default.aspx

This example specifies that the Russian language and culture settings are used for everything on the page. You can see this in action by using this @Page directive and a simple calendar control on the page. Figure 27-4 shows the output. Notice that marking the page as using Russian settings does not automatically translate text within the page; it only updates the embedded control added to the page.

![](img/d99870e80390742f93963da7be0b2e61_911_0.png)

FIGURE 27-4

## Adopting Culture Settings in ASP.NET

In addition to using server-side settings to define the culture for your ASP.NET pages, you also have the option to define the culture according to what the client has set as his or her preference in a browser instance.

When end users install Microsoft’s Internet Explorer or some other browser, they have the option to select their preferred cultures in a particular order (if they have selected more than a single culture preference). To see this in action in IE, select Tools → Internet Options
