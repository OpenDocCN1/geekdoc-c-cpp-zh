required attribute. Note that for non-server elements, like plain HTML elements, the runat attribute is optional. With this attribute, non-server controls can be reached by your programming code. You learn more about this later in the book.

You can easily add the runat attribute to an existing element using a code snippet by typing runat and pressing the Tab key.

The preceding example of the TextBox uses a self-closing tag where the closing slash (/) is embedded in the opening tag. This is quite common for controls that don't need to contain child content such as text or other controls. However, the long version, using a separate closing tag, is acceptable as well:

```
<asp:TextBox ID="Message" runat="server"></asp:TextBox>
```

You can control the default behavior of closing tags per element using Tools ⌃ Options ⌃ Text Editor ⌃ HTML ⌃ Formatting ⌃ Tag Specific Options.

You can program against this text box from code that is either placed inline with the page or in a separate Code Behind file, as you saw in Chapter 2. To set the welcome message and the time, you can use the following code:

# VB.NET

```
Message.Text = "Hello World, the time is " & DateTime.Now.TimeOfDay.ToString()
```

# C#

```
Message.Text = "Hello World, the time is " + DateTime.Now.TimeOfDay.ToString();
```

The definition of the control in the markup section of the page is now separated from the actual code that defines the text displayed in the text box, making it easier to define and program the text box (or any other control) because it enables you to focus on one task at a time. You can either declare the control and its visual appearance in the markup section of the page, or program its behavior from a code block.

In general, controls defined in Markup View are not case-sensitive, although some of the values you can set are case-sensitive. I prefer to use the capitalization as suggested by IntelliSense. Note that when using C#, properties you use in the Code Behind are case-sensitive.

You see how server controls send their underlying HTML to the client in the next exercise.

# TRY IT OUT Working with Server Controls

In this exercise, you add a TextBox, a Label, and a Button control to a page. When you request the page in the browser, these server controls are transformed into HTML, that is then sent to the client. By looking at the final HTML for the page in the browser, you'll see how the HTML is completely different from the initial ASP.NET markup.

+   1. Open the Planet Wrox project in Visual Studio.
+   2. In the Demos folder in the Solution Explorer, create a new Web Form called ControlsDemo.aspx. Choose your programming language and make sure the Web Form uses Code Behind.