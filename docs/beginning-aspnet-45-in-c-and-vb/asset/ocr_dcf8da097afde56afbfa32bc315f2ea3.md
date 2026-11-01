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