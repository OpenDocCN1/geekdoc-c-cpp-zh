
2. View the HTML for the page in the browser by right-clicking the page and choosing View Source or View Page Source.

3. Locate the input field for the user's name and then look at the code for the validator that is placed directly below it. You should see something like this:

```
<span id="cpMainContent_ContactForm_RequiredFieldValidator1" class="ErrorMessage" style="visibility:hidden;"></span>
```

4. Scroll down to the end of the code until you see the large chunk of JavaScript code that is responsible for the validation. For the Name field, you'll see something like this:

```
var cpMainContent_ContactForm_RequiredFieldValidator1 = document.all ?
    document.all["cpMainContent_ContactForm_RequiredFieldValidator1"] :
    document.getElementById("cpMainContent_ContactForm_RequiredFieldValidator1");
cpMainContent_ContactForm_RequiredFieldValidator1.controltovalidate
    = "cpMainContent_ContactForm_Name";
cpMainContent_ContactForm_RequiredFieldValidator1.errormessage
    = "Enter your name";
cpMainContent_ContactForm_RequiredFieldValidator1.evaluationfunction
    = "RequiredFieldValidatorEvaluateIsValid";
cpMainContent_ContactForm_RequiredFieldValidator1.initialvalue = "";
```

For each of the validation controls you see similar code, all adding to the size of the page.

5. Go back to VS, right-click the website in the Solution Explorer, and choose Add ▸ Add New Item. Locate the Global Application Class item. You don't have to enter a name because the default of Global.asax is the only allowed name for this file.

6. Add the following code to the Application_Start method that is already part of the code template of the Global.asax file:

```
VB
Sub Application_Start(ByVal sender As Object, ByVal e As EventArgs)
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        New ScriptResourceDefinition With
        {
            .Path = "~/Scripts/jquery-1.7.2.min.js"
        })
End Sub
```

```
C#
void Application_Start(object sender, EventArgs e)
{
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        new ScriptResourceDefinition
        {
            Path = "~/Scripts/jquery-1.7.2.min.js"
        });
}
```

The spelling of the word jquery (all lowercase) is case sensitive, so make sure you type it exactly as shown here. If you have a newer version of the jQuery library, don't forget to update the version number.

7. Save your changes and close the file.

8. Next, open up the Web.config file and modify the following line of code in the <appSettings> element. You added that line in Chapter 9. If you don't have this line of code, add it between the <appSettings> tags. Either way, you should end up with this code:

```
<appSettings>
...
    <add key="ValidationSettings:UnobtrusiveValidationMode" value="WebForms" />
</appSettings>
```

9. Open up the master page and change the reference to the jQuery library so it points to the ScriptResourceDefinition you created in the Global.asax file like this:

```
<asp:ScriptManager ID="ScriptManager1" runat="server" EnablePageMethods="true">
    <Scripts>
        <asp:ScriptReference Name="jquery" />
    </Scripts>
</asp:ScriptManager>
```

If you didn't make this change, jQuery would be included twice on pages that use the validation controls; once from the code in Global.asax, and once from the reference in the ScriptManager control. By having the ScriptReference point to the ScriptResourceDefinition defined in Global.asax, ASP.NET sees that it's pointing to the same JavaScript library and includes the reference only once.

10. Save your changes and then request Contact.aspx in your browser. Click the Send button and notice that validation still works. Open up the HTML for the page and locate the input field for the name again. Below the field you should see the following code for the validator:

```
<span data-val-controltovalidate="cpMainContent_ContactForm_Name"
      data-val-errormessage="Enter your name"
      id="cpMainContent_ContactForm_RequiredFieldValidator1"
      class="ErrorMessage" data-val="true"
      data-val-evaluationfunction="RequiredFieldValidatorEvaluateIsValid"
      data-val-initialvalue="" style="visibility:hidden;">*</span>
```

11. Scroll down to the end of the code. Notice all the JavaScript you saw previously has now gone. Instead, at the top of the file you now find a <script> element that points to a JavaScript file (one of the links that start with /ScriptResource.axd) that contains validation code that uses the jQuery library.

## How It Works

By enabling unobtrusive JavaScript validation, the validation controls generate different code. Rather than emitting JavaScript code that carries out the validation, the controls now emit HTML5 data attributes on the validation <span>. The HTML5 specification enables you to make up your own attributes on elements as long as you prefix them with data-. The unobtrusive validation framework makes use of this feature by adding attributes for things like the error message (in data-val-error-message), and the JavaScript function that needs to be executed to validate the input control (in data-val-evaluationfunction). When you click the submit button, the validation framework kicks in, finds all controls that need to be validated, and then uses the data- attributes to determine what needs to be validated and how. Note that other than the validation controls and the JavaScript they generated

previously, not much has changed. Your page still contains the same input controls and submit button. But the way validation takes place has changed radically, and now uses the jQuery library and the data-attributes added to the HTML elements.

To enable unobtrusive validation you have to enable a key in Web.config that you previously disabled. This key signals the validation framework to switch modes and emit unobtrusive JavaScript code instead. Because the validation relies on jQuery, you also need to register the jQuery library with the ScriptManager. Unfortunately, you cannot register the library with the ScriptManager control; you have to do this in the Global.asax with this code:

```
VB
Sub Application_Start(ByVal sender As Object, ByVal e As EventArgs)
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        New ScriptResourceDefinition With
        {
            .Path = "~/scripts/jquery-1.7.2.min.js"
        })
End Sub
```

```
C#
void Application_Start(object sender, EventArgs e)
{
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        new ScriptResourceDefinition
        {
            Path = "~/scripts/jquery-1.7.2.min.js"
        });
}
```

This code uses an object initializer to create a new instance of the ScriptResourceDefinition class. It sets its Path property to the path of the jQuery library. This instance is then added to the ScriptManager's ScriptResourceMapping using the AddDefinition method. Finally, by pointing the ScriptManager control in the master page to this ScriptResourceDefinition, jQuery is included on all pages in your site. Although this looks a bit funky, the outcome is pretty straightforward: a link to the referenced jQuery library is added to the output of the page so the validation framework can use it.

Once you've set this up, you never have to worry about it; you can add validation controls to your page as you did before and jQuery and the validation framework of ASP.NET will handle all validation for you. Note that this change does not impact server-side validation at all; that will continue to function as before.

If by now you think that jQuery really rocks, I completely agree. Although it may be a bit difficult to get used to jQuery in the beginning, once you get the hang of it you'll wonder how you ever did without it. And what's even cooler is that you're not limited to what the jQuery library supports out of the box. jQuery has a pluggable architecture, which means you can write plug-ins for it that extend or enhance jQuery's functionality. At the time of writing, the official jQuery plug-in site was taken offline while they were working on a new site. However, searching the web for "jQuery plug-ins" should bring up many useful plug-ins for all kinds of purposes, ranging from image galleries, validation frameworks, visual tooltips, dialog boxes, and more. You're also encouraged to
