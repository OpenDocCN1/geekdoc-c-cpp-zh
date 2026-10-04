attribute is optional. With this attribute, non-server controls can be reached by your programming code. You learn more about this later in the book.

You can easily add the runat attribute to an existing element using a code snippet by typing runat and pressing the Tab key.

The preceding example of the TextBox uses a self-closing tag where the closing slash (/) is embedded in the element, which is common for controls that don't need to contain child content as text or other controls. However, the long version, using a separate closing tag, is acceptable as well:

```
<asp:TextBox ID="Message" runat="server"></asp:TextBox>
```

You can control the behavior of closing tags by editing using Tools > Options > Text Editor > HTML (Web Forms) > Formatting > Tag Options.

You can program against this text box from either placed inline with the page or in a separate Code Behind as shown in Chapter 2. Then to see the welcome message and the time, you can use the following:

```
VB.NET
Message.Text = "Hello World, the time is " & DateTime.Now.TimeOfDay.ToString()
C#
Message.Text = "Hello World, the time is " + DateTime.Now.TimeOfDay.ToString();
```

The definition of the control in the markup section of the page is now separated from the actual control that defines the text displayed in the text box, making it easier to define and program the text box (or any other control) because it allows you to focus on one at a time. You can either declare the control and its visual appearance in the markup section of the page, or program its behavior from a code block.

In general, controls defined in Markup View are not case-sensitive, although some of the values you can set are case-sensitive. I prefer to use the capitalization as suggested by IntelliSense. Note that using C#, properties you use in the Code Behind are case-sensitive.

You see how server controls send their underlying HTML to the client in the next exercise.

# TRY OUT Working with Server Controls

In this exercise, you add a TextBox, a Label, and a Button control to a page. When you refresh the browser, these server controls are transformed into HTML that is sent to the client. By looking at the final HTML for the page in the browser, you'll see how the HTML is completely different from the initial ASP.NET markup.

+   1. Open the Panel project in Visual Studio.

+   2. In the Demos folder in the Solution Explorer, create a new Web Form called Demo.aspx. Choose your programming language and make sure the Web Forms use Code Behind.

+   3. Switch to Design View. From the Standard category of the Toolbox, drag a TextBox, a Button, and a Label control onto the design surface within the dashed lines of the <div> tag that was added for you when you created the page.