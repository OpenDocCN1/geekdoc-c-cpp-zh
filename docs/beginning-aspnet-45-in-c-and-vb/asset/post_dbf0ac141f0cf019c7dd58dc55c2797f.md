
To give you an idea of how the validation controls work, the following exercise guides you through the process of using the RequiredFieldValidator in a contact form that is placed in a user control. The exercise is followed by an in-depth discussion of the various validation controls.

> NOTE Visual Studio comes with a number of useful code snippets that enable you to quickly insert controls like the validation controls in Markup View. In the following exercise, you see how to add the necessary controls using the Toolbox, Design View, and drag and drop, but it's useful to know how to quickly add controls in Markup View as well. For example, to insert a TextBox in Markup View, type tb or textbox and then press Tab. VS completes the full control code for you. To insert a RequiredFieldValidator, type the letters req, press Ctrl+Spacebar to have VS complete the word requiredfieldvalidator for you, and then press Tab again to insert the entire tag.
> 
> If you do this directly below a TextBox control with its ID set, VS even sets the correct ControlToValidate attribute for you. This latter trick wouldn't work if you tried it in the next exercise because the various controls are not directly next to each other, but are placed in separate table cells. VS still inserts the code for the RequiredFieldValidator for you, but you need to set the ControlToValidate property to the ID of the associated TextBox manually.

## TRY IT OUT Using the RequiredFieldValidator

In this exercise, you create a user control called ContactForm.ascx. You can place it in a web page so visitors to your site can leave some feedback. In later exercises, you extend the control by sending the response by e-mail to your e-mail account.

- 1. Open the Planet Wrox project and add a new user control in the Controls folder. Call the control ContactForm.ascx. Make sure that it uses your programming language and a Code Behind file.
- 2. Switch to Design View and insert a table by choosing Table ⇨ Insert Table. Create a table with eight rows and three columns.
- 3. Merge the three cells of the first row. To do this, select all three cells, right-click the selection, and choose Modify ⇨ Merge Cells.
- 4. In the merged cell, type some text that tells your users they can use the contact form to get in touch with you. You could use an h1 element as a heading above the page to draw the user's attention.
- 5. In the first cell of the second row, type the word Name. Into the second cell of the same row, drag a TextBox and set its ID to Name. Into the last cell of the same row, drag a RequiredFieldValidator from the Validation category of the Toolbox. Finally, into the second cell of the last row, drag a Button. Rename the button to SendButton by setting its ID and set its Text property to Send. When you're done, your Design View looks like Figure 9-3.

![](img/eadab2ccd79b253c01a3fdff2321202d_361_0.png)

## FIGURE 9-3

- 6. Click the RequiredFieldValidator once in Design View and then open up its Properties Grid by pressing F4. Set the following properties on the control:

| PROPERTY | VALUE |
|---|---|
| CssClass | ErrorMessage |
| ErrorMessage | Enter your name |
| Text | * |
| ControlToValidate | Name |

Note: you can type in the value for ControlToValidate directly or you can pick it from the list by clicking the down arrow.

- 7. Save the changes to the user control and then close it because you're done with it for now.

- 8. Add the following CSS declaration to the CSS files for both themes (Monochrome.css and DarkGrey.css):

```
.ErrorMessage
{
    color: Red;
}
```

Save and close both files.

- 9. Open Contact.aspx from the About folder in Markup View and from the Solution Explorer, drag the user control ContactForm.ascx between the tags of the cpMainContent control. You should end up with this control declaration:

```
<asp:Content ID="Content2" ContentPlaceHolderID="cpMainContent" runat="Server">
<Wrox:ContactForm ID="ContactForm" runat="server" />
</asp:Content>
```

Visual Studio remembers the last custom prefix you used and reuses that when dragging the user control onto the page. Depending on how you previously configured the Banner user control in Web.config, your prefix may be different. That doesn’t matter for this exercise. Also note, when you drag the control in Design View, its ID is ContactForm1. For this exercise, the actual ID doesn’t matter, but beware of the difference when working with the control ID later in this chapter.

- 10. Open Web.config and add or modify the following code under the <appSettings> element (which is a direct child of the main <configuration> node):

```
<configuration>
  <appSettings>
    <add key="ValidationSettings:UnobtrusiveValidationMode" value="None" />
  </appSettings>
  ...
</configuration>
```

Unobtrusive validation requires jQuery, which is discussed in Chapter 11. Until then, you need to disable it or your pages with validation controls will throw errors.

- 11. Save your changes and open Contact.aspx in your browser. If you get an error, make sure you renamed the TextBox to Name and that you set the ControlToValidate property on the RequiredFieldValidator to Name.

- 12. Leave the Name text box empty and click the Send button. Note that the page is not submitted to the server. Instead, you should see a red asterisk appear at the very right of the row for the name field to indicate an error. If the asterisk is not red, press Ctrl+F5 or Ctrl+R to get a fresh copy of the theme’s CSS file from the server and click the Send button again.

- 13. Enter your name and click Send again. The page now successfully posts back to the server.

## How It Works

With the RequiredFieldValidator attached to the TextBox through the ControlToValidate property, client-side JavaScript is sent to the browser that validates the control at the client.

The RequiredFieldValidator control is able to validate another control like a TextBox. It does this by comparing the value of the other control with its own InitialValue property and making sure that the other control’s value is different. By default, this property is an empty string, which means that anything except an empty string is considered a valid value. Whenever you try to submit the form to the server by clicking the Send button, the validation control checks the control it is attached to. When the text box is still empty, the asterisk from its Text property is shown (formatted with the ErrorMessage CSS class), and the form is not submitted. You see how to use and display the ErrorMessage property later in this chapter. When the user enters something in the Name text box, validation succeeds and the page submits to the server successfully.

## Using the HTML5 Data Types

HTML5 has introduced a number of new types for the type attribute on the input element. These new types enable you to determine how a browser should interpret the field so it can render a correct
user interface for it. ASP.NET 4.5 supports these new attributes using the TextMode property of a TextBox control. In addition to the SingleLine, MultiLine, and Password types that have been supported since ASP.NET 1, you can now use the following values as well:

| VALUE | DESCRIPTION |
|---|---|
| Color | Enables the user to choose a color, usually from a color picker. |
| Date / DateTime / DateTimeLocal / Month / Week / Time | Enables various ways for the user to enter a date or time. Depending on the type, the browser renders a calendar or other specialized control to enter a value. |
| Email | Enables the user to enter an e-mail address. |
| Url | Enables the user to enter a web address. |
| Number | Enables the user to enter a number. |
| Range | Enables the user to enter a number with a specified range. The browser typically draws a slider control to enter the value. |
| Search | Enables the user to enter a search term. This typically renders a standard text box but with an option in the right corner to clear the text. |

These server-side values for the TextMode property are converted into client-side HTML attributes with the same name, but written in lowercase. To see how that looks, consider this TextBox:

```
<asp:TextBox runat="server" ID="Email" TextMode="Email" />
```

When rendered in the browser, this control generates the following HTML:

```
<input name="Email" type="email" id="Email" />
```

Based on various values for the type attribute, browsers can help the user enter the correct data by drawing a different user interface for the control and by validating the data that is entered. Also, devices with a "soft keyboard"—a keyboard that is displayed on-screen—are able to adapt the keyboard to match the data type for the input control. For example, Apple's iPad shows a numeric keyboard if you put the focus on a text box with its type set to number.

Although these new attribute values are a great addition to HTML5, you need to be aware of a few caveats. First of all, with HTML5 being so new, not all browsers support these new features. Figure 9-4 shows each of these attributes in the five most popular browsers today. On the first row, you see Internet Explorer 10, Firefox 14, and Chrome 21; and on the second row, you see Safari 5 and Opera 12.

As you can see, some browsers support more of the attributes than others. At the time of writing, Opera and Safari have the best support. Note that not all browsers implement these new types exactly the same. For example, in Firefox you'll get an error and you won't be able to submit the page if you enter a value that doesn't look like an e-mail address in an input box with its type attribute set to email.

Another thing you need to realize is that you should see these new attributes as helpful hints to the user only; you should never solely rely on them for validation purposes. It would be easy for a
