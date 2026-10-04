
## WHAT YOU LEARNED IN THIS CHAPTER

|  |  |
|---|---|
| CSS | Cascading style sheets, the language used to lay out web pages in the browser. |
| CSS Box Model | The model on which the dimensions of elements are calculated with regard to height, width, padding, border, and margin. |
| Declaration | A combination of a property and a value that determines the styling for the element to which the declaration applies. |
| Embedded style sheets | CSS code that is defined in a page in a <style /> element. Usually referred to as embedded styles. |
| External style sheets | CSS code that is defined in a separate file and then included in a page using the <link /> element. |
| Inline style sheets | CSS code that is defined directly on an element using the style attribute. Usually referred to as inline styles. |
| Rule set | A combination of a selector and one or more declarations wrapped in a pair of curly braces. |
| Selector | A CSS construct to point to one or more elements in the page. Different selectors exist, including the Universal selector, the ID and Class selectors, and the Type selector. |

## 4
Working with ASP.NET Server Controls

WHAT YOU WILL LEARN IN THIS CHAPTER:

- What ASP.NET Server Controls are
- The different kinds of server controls you have at your disposal
- The common behavior shared among most of the server controls
- How the ASP.NET run time processes the server controls on your page
- How server controls are able to maintain their state across postbacks

WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/go/begaspnet451. The code is in the Chapter 4 folder.

ASP.NET Server Controls are the workhorses of all the Web Forms pages you build in Visual Studio. VS will contain one or more server controls. These controls are in all sorts and sizes, ranging from simple controls like a Button and a Label to complex controls like the GridView and the ListView that are capable of displaying data from a data source (like a database or an XML file). You see these controls in Chapters 7, 13, and 14.

The architecture of ASP.NET Server Controls is deeply integrated into ASP.NET, giving the controls a feature set that is unique in today's technologies for building websites. This chapter shows you what server controls are, how they work, and which ones are available out of the box when you install VS.

The chapter starts off with a general discussion of server controls. You see how to define them in your code by adding them to Design or Markup View.

The section that follows gives you a thorough look at the controls that are available in the VS Toolbox.

### INTRODUCTION TO SERVER CONTROLS

It's important to understand how server controls operate and how they are completely different from the way you define controls in other languages like classic ASP or PHP (another popular programming language for creating dynamic websites).

For example, to influence the text in a text box in these languages, you would use HTML and mix it with server-side code. This works similarly to the example in Chapter 2 where the current date and time are displayed on the page. To create a text box with a message and the current time in it classic ASP, you can use the following:

```
<input type="text" value="Hello World, the time is <%=Time()%> />
```

As you can see, this code contains HTML, mixed with a server-side code, delimited by <%= %> that outputs the current time using the Time() function. This type of coding has a major disadvantage: the HTML and server-side code is mixed, making it difficult to maintain your pages. Although it is still easy to understand the code, this type of programming can quickly result in messy and complex pages.

Server controls work differently. In ASP.NET, the controls "live" on the server inside an ASPX page. When the page is requested by the browser, the server-side controls are processed by the ASP.NET run time for ASPX pages. The controls then emit client-side HTML code that is appended to the final page output. This HTML code eventually ends up in the browser, where it is used to build up the page.

So, instead of defining HTML controls in your pages, you define an ASP.NET Server Control with the following syntax, where the italicized parts differ for each control:

```
<asp:TypedControl ID="Name" runat="server" />
```

For those with ASP.NET you use the asp: prefix before the control name. For example, to create a TextBox that holds the same message and current time, you can use the following syntax:

```
<asp:TextBox ID="Message" runat="server" />
```

Note that the control has two attributes: ID and runat. The ID attribute is used to uniquely identify a control on the page, so you can ensure the ASP.NET understands what control you're referring to. It has a unique ID; if you accidentally type a duplicate control ID, VS signals the problem in the error list. The mandatory runat is used to indicate that this is a control that lives on the server. Without this attribute, the controls won't be processed and will end up directly in the HTML source. If you feel you're missing a control in the final output in the browser, ensure that the control has this required attribute. Note that for non-server elements, like plain HTML elements, the runat

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

### TRY OUT Working with Server Controls

In this exercise, you add a TextBox, a Label, and a Button control to a page. When you refresh the browser, these server controls are transformed into HTML that is sent to the client. By looking at the final HTML for the page in the browser, you'll see how the HTML is completely different from the initial ASP.NET markup.

- 1. Open the Panel project in Visual Studio.
- 2. In the Demos folder in the Solution Explorer, create a new Web Form called Demo.aspx. Choose your programming language and make sure the Web Forms use Code Behind.
- 3. Switch to Design View. From the Standard category of the Toolbox, drag a TextBox, a Button, and a Label control onto the design surface within the dashed lines of the <div> tag that was added for you when you created the page.
