# VB.NET

Dim age As Integer = Convert.ToInt32(Age.Text) ' age now holds the user's age

# C#

```
int age = Convert.ToInt32(Age.Text); // age now holds the user's age
```

Note in this case, there is no need to access a collection like Form as you saw with the QueryString collection earlier. ASP.NET shields you from the complexity of manually retrieving data from the submitted form, and populates the various controls in your page with data from the form. If you need to, you can still access the form values by accessing the Request.Form collection, similar to how you do it with the Request.QueryString collection.

With the previous code example, it as well as users enter values like an age in the text box. But what happens when a user submits invalid data, deliberately or by accident? What if a user enters the text I am 42 instead of the number 42? When that happens, the code will crash. The ToInt32 method of the Convert throws an exception (an error) when you pass something that cannot be represented as a number. As soon as the exception is thrown, page execution stops completely. 18 days into deep exception handling.

To avoid these problems, you need to validate all the data that is being sent to the server. When it doesn't look like, you need to reject it and make sure your application deals with gracefully.

# Validating Input in Web Forms

People concerned with validating user input often use the mantra: Never trust user input. This may seem paranoia at first, but it is really important in any open system. Even if you know who your users are, and if you trust them completely, they are not the only users who can access your system. As soon as your site is out on the Internet, it is a potential target for malicious users and hackers who will try to find a way into your system. In addition to these evil visitors, your users may send incorrect data to your server by accident.

To help you as much as possible, ASP.NET ships with a range of validation controls that help you validate data before it is used in your application. In the following sections, you will see how to use the standard validation controls to ensure the user submits valid data into the system.

# The ASP.NET Validation Controls

ASP.NET 4.5.1 has several useful controls to perform validation in your website. Five of them are used to perform the actual validation, whereas the final — ValidationSummary — is to provide feedback about any errors made in the page. Figure 9-1 shows the available controls in the Validation category of Toolbox.

The validation controls are extremely helpful in validating the data that a user enters in the system. They can be easily hooked to other controls like the TextBox or a DropDownList; however, they also support validation scenarios. Figure 9-2 demonstrates two of the validation controls — RequiredFieldValidator and RangeValidator at work to prevent a user from submitting the form without enough required and valid data.

| Toolbox |
| Search Toolbox |
| Standard |
| Data |
| Printer |
| CompareValidator |
| CustomValidator |
| RangeValidator |
| RegularExpressionValidator |
| RequiredFieldValidator |
| ValidationSummary |

FIGURE 9-1