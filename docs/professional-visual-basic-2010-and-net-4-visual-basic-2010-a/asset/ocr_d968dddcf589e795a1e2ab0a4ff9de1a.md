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

![](bbox=[0.487, 0.455, 0.878, 0.71])

In this example, only a couple of lines of code are changed to assign a new instance of the CultureInfo object to the CurrentCulture property of the thread being executed by the application. The culture setting enables the CultureInfo object to define the culture you want to utilize. In this case, the Thai language of Thailand is assigned. The results produced in the TextBox control are illustrated in Figure 27-3.

From this figure, you can see that the .NET Framework provides the native name of the language used even if it is not a Latin-based letter style. In this case, the results are presented for the Thai language in Thailand, including some of the properties associated with this culture (such as an entirely different calendar than the one used in Western Europe and the United States).

# Declaring Culture Globally in ASP.NET

ASP.NET enables you to easily define the culture that is used either by your entire ASP.NET application or by a specific page within your Web application, using what are termed *server-side culture declarations*. You can specify the culture for any of your ASP.NET applications by means of the appropriate configuration files. To demonstrate this, close the ProVB2010_Localization application you started with and create a new ASP.NET website called ProVB_Russian. Alternatively, you can open this download folder as a website in Visual Studio 2010. On the default.aspx page add a new Calendar control from the toolbox, following the text: Welcome to ASP.NET!