# JQUERY VALIDATION

Remember the validation controls you used in Chapter 9 to validate the contact form? The validation controls work by generating JavaScript that is added to the page. The downside of this approach is that your page becomes unnecessarily large a lot of repetitive code is added to each page that uses these controls. Developers of ASP.NET have thought of this and decided to leverage the power of jQuery to improve client-side validation. They have done this through a concept known as unobtrusive JavaScript, where the functionality (the code that gets executed) has been separated from the structure and content of the page. Rather than embedding large chunks of JavaScript code in the page, they have written a small JavaScript library that uses jQuery to perform the validation. This leads to cleaner code and reduces the size of the page. For the Contact Us page, enabling unobtrusive JavaScript decreased the size of the final HTML from 20.7KB to 14.9KB, a reduction of more 25 percent.

Configuring the validation framework to use unobtrusive validation with jQuery instead of the built-in code that is generated is a three-step activity:

+   1. Enable unobtrusive validation in the Web.config file.
2. Register the jQuery library with the ScriptManager in the Global.asax file.
3. Install a package that contains JavaScript files to handle the client side validation.

In the next exercise you will see how to add the Global.asax file to your site and then enable unobtrusive JavaScript validation.

# TRY OUT Enabling Unobtrusive JavaScript Validation

In this exercise you revisit the current Contact Us page to look at the code that the controls generate. You'll then modify the Global.asax file and enable unobtrusive validation so you can see the effect on the code that is generated.

+   1. Start by opening the Contact.aspx file from the About folder and then press Ctrl+F5 to view your page in browser.

+   2. View the HTML for the page by right-clicking the page and choosing View Source or View Page Source.

+   3. Locate the input field for the user's name and then look at the code for the validator that is placed directly below it. You should see something like this:

```
<span id="cpMainContent_ContactForm_RequiredValidator1" class="ErrorMessage" style="visibility:hidden;">*</span></span>
```

Scroll down to the end of the code until the unit you see the large chunk of JavaScript code that is responsible for the validation. For the Name, you'll see something like this:

```
var cpMainContent_ContactForm_RequiredValidator1 = document.all ? \
document.["cpMainContent_ContactForm_RequiredValidator1"] : \
document.getElementById("cpMainContent_ContactForm_RequiredValidator1").controlitvalidate = \
cpMainContent_ContactForm_RequiredValidator1.controlname = \
*"cpMainContent_ContactForm_Name";
```