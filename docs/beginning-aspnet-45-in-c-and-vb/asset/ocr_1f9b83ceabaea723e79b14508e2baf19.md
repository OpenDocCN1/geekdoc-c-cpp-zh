```
{
    args.isValid = false;
}
</script>
<table class="auto-style1">
```

In JavaScript, it's common to write method names using camel casing, where the first word of the method name is written in lowercase, followed by words with the first letter in uppercase.

If you find that VS is adding your opening curly braces ({}) at the end of a line, rather than on their own line, choose Tools ⇨ Options from the main menu. Then expand the path Text Editor ⇨ JavaScript ⇨ Formatting and check off both items in the New Lines category. This is purely a formatting preference; the JavaScript runs fine with or without the curly brace on its own line. Note that JavaScript is case sensitive, so make sure you type the code exactly as shown here.

7. Save all the changes by pressing Ctrl+Shift+S, request the Contact.aspx page in your browser, and click the Send button. Also note that the ValidationSummary control shows a list of all the problems with the data entered in the form. The client-side JavaScript function validatePhoneNumbers now ensures that you enter at least one phone number before you can submit the page back to the server. Figure 9-8 shows how the page appears in Google Chrome.

![](bbox=[0.16, 0.63, 0.88, 0.87])

FIGURE 9-8

8. Go back to VS and click the ValidationSummary control in Design View. On the Properties Grid, change ShowMessageBox to True and ShowSummary to False. (Quick tip: you can easily choose