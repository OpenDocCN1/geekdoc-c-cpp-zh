
## Adding Your Own Information to the Trace

Adding your own data to the trace is useful if, for example, you want to see the value of a variable, or want to find out if a specific event fires, and when it fires exactly.

You can add information to the trace by using the Trace class. This class exposes two useful methods: Write and Warn. Both do pretty much the same thing: they add information to the trace that you can optionally put in a category you make up yourself. The only difference between Write and Warn is that messages written by Warn appear in red. You could use the Warn method for unexpected situations because the message will draw more attention.

In the following exercise, you will see how simple it is to add your own information to the trace using the Warn and Write methods.

### TRY IT OUT  Adding Trace Data to Your Pages

In this Try It Out, you add some custom information to the ASP.NET trace. You use the Write method to write out trace information in a normal page execution, and use the Warn method for unexpected scenarios.

- 1. Open CalculatorDemo.aspx, switch to its Code Behind, and locate the Click handler for the Calculate button.
- 2. Right before the Select Case (VB.NET) or switch statement (C#), add the following Trace.Write call:
- 3. Near the bottom of the event handler, modify the Else statement for the check that ensures that both TextBox controls contain a value:

```VB.NET
Trace.Write(String.Format("Performing the calculation with the {0} operator", OperatorList.SelectedValue))
Select Case OperatorList.SelectedValue
```

```C#
Trace.Write(string.Format("Performing the calculation with the {0} operator", OperatorList.SelectedValue));
switch (OperatorList.SelectedValue)
```

```VB.NET
Else
  Result.Text = String.Empty
  Trace.Warn("Custom Category", "TextBox controls are empty; time to add Validation controls?")
End If
```

```C#
else
{
```

### EXERCISES

- 1. What's the difference between debugging and tracing?
- 2. Imagine you have some code that could potentially throw an exception. For example, you try to send an e-mail message to a mail server. What kind of exception-handling strategy would you use to avoid the exception from being displayed in the browser? What code would you need?
- 3. You're taking over a website that has been built by another developer who had never heard of exception handling. Your client is complaining about the quality of the site and the large number of "Yellow Screens of Death" that users see. Besides analyzing the code for the entire application, what would be a quick solution to get information about the errors and the locations where they occur? And how can you shield the site's users from the dirty details of the exception messages?

You can find answers to these exercises in Appendix A.

### WHAT YOU LEARNED IN THIS CHAPTER

| Term | Definition |
|---|---|
| Breakpoint | A marker you can set in your code to indicate where you want the debugger to halt at run time |
| Data tips | Tooltips that present simple or rich data about variables during debugging |
| Debugging | The process of finding and fixing bugs in your code |
| Exception | The .NET term for an error that may occur in your code |
| Exception handling | A methodology to identify and handle errors that occur at run time |
| Stack trace | A visual representation of the current stack of code calls |
| Trace | Enables ASP.NET controls and your own custom code to write information to a central log location at run time |

![](img/eadab2ccd79b253c01a3fdff2321202d_774_0.png)

## Deploying Your Website

### WHAT YOU WILL LEARN IN THIS CHAPTER:

- How to ease the deployment process through simple changes to your code and configuration
- How to prepare your site for deployment by creating a copy using Visual Studio's built-in copy tools
- How to install and configure a web server and your website on your target machine
- How to avoid common errors you may get when deploying a site
- How to copy data stored in your SQL Server database to the target server

### WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/remtitle.cgi?isbn=1118311809. The code is in the Chapter 19 download.

Congratulations! The fact that you're reading this chapter probably means you now have a full-featured, database-driven ASP.NET website that is ready for release into the wild. It's an exciting time for you and your project. Pretty soon your application will be used and judged by your target audience.

To make your website accessible to users worldwide, you need to publish it to a production server that is connected to the Internet. What kind of server this is and where it is located depends on your own requirements and budget. You can host the site on a home server in your attic with a private Internet connection (as I used to do with http://imar.spaanjaars.com) or you can host it with an external (and often commercial) party with a direct connection to the Internet backbone.

Fortunately, ASP.NET comes with a great solution to avoid these kinds of problems: the Web.config file, expression syntax, and the WebConfigurationManager class you use to read from Web.config.

### The Web.config File

You've used the Web.config file a number of times in this book to store information about connection strings, membership, roles and profile information, and more. You also briefly saw the <appSettings> element that enables you to store data in a key/value pair using <add> elements. The <appSettings> element enables you to store simple information, such as an e-mail address, and retrieve that value by its key. For example, to store an e-mail address, you can add the following to the Web.config file:

```
<appSettings>
  <add key="FromAddress" value="webmaster@example.com" />
</appSettings>
```

The <appSettings> element is placed outside the <system.web> element in the Web.config file, yet still within the parent <configuration> element.

Obviously, you need a way to access the data in <appSettings> at run time. You can do this in a couple of ways, including expression syntax and the WebConfigurationManager class, both of which are discussed next.

### Expression Syntax

Expression syntax enables you to bind control properties to resources, such as those found in the <appSettings> element in Web.config, connection strings, localization resource files, and various routing settings used in URL rewrite scenarios. To display data from the <appSettings> element, you use the following syntax, where AppSettingKeyName refers to a key you define in Web.config:

```
<%$ AppSettings:AppSettingKeyName %>
```

For example, to display a copyright notice on your pages in a Literal control, you can add the following setting to Web.config:

```
<add key="Copyright" value="Copyright by Wrox" />
```

You can then display this text in a Literal control like this:

```
<asp:Literal ID="Copyright" runat="server" Text="<%$ AppSettings:Copyright %>" />
```

To make it even easier to set properties like Text as in the preceding example, Visual Studio comes with the Expression Editor. To access this dialog box, select a control in Design or Markup View, open its Properties Grid, and click the ellipsis for the (Expressions) item, shown in Figure 19-1. You may find that the (Expressions) item does not always show up when in Markup View. If that's the case, switch to Split View or Design View first.

The Expressions dialog for the Literal control opens, enabling you to bind control properties to expressions. Visual Studio limits the list of properties of the control to those that can be bound using an expression. To bind the Text property of the Literal control to an application setting,
