
## Adventure Works Customers

| ID | Title | First Name | Last Name |
| --- | --- | --- | --- |
| 1 | Mr. | Orlando | Gee |

Email: orlando0@adventure-works.com

Phone: 245-555-0173

3. In the bottom command bar, click the Edit Customer button.

4. The buttons in the top command bar become disabled because the ViewModel is now in Editing mode. Additionally, the Add and Edit buttons are also disabled, but the Save and Discard buttons should now be enabled. Furthermore, the data entry fields on the form should now be enabled, and the user can modify the details of the customer.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_871_0.png)

5. Modify the details of the customer: blank out the first name, type Test for the email address, type Test 2 for the phone number, and then click Save. These changes violate the validation rules implemented by the ValidateCustomer method. The ValidateCustomer method populates the LastError property of the ViewModel with validation messages, which are displayed on the form in the TextBlock that binds to the LastError property:

## Adventure Works Customers

ID
1

Title
Mr.

First Name

Last Name
Gee

Email
Test

Phone
Test 2

First Name must not be empty
Invalid Email Address
Invalid Phone Number

6. Click Discard, and verify that the original data is reinstated on the form. The validation messages disappear, and the ViewModel reverts to Browsing mode.

7. Click Add. The fields on the form should be cleared (apart from the ID field, which displays the value 0). Enter the details for a new customer. Be sure to provide a first name and last name, a valid email address of the form name@organization.com, and a numeric phone number (you can also include parentheses, hyphens, and spaces).

8. Click Save. If the data is valid (there are no validation errors), your data should be saved to the database. You should see the ID generated for the new customer in the ID field, and the ViewModel should switch back to Browsing mode.

9. Experiment with the app by adding and editing more customers. Notice that you can resize the view to display the columnar layout, and the form should still work.

10. When you finish, return to Visual Studio and stop debugging.

## Summary

In this chapter, you learned how to use the Entity Framework to create an entity model that you can use to connect to a SQL Server database. The database can be running locally or in the cloud. You also saw how to create a REST web service that a UWP app can use to query and update data in the database through the entity model, and you learned how to integrate code that calls the web service into a ViewModel.

You have now completed all the exercises in this book. I hope you are thoroughly conversant with the C# language and understand how to use Visual Studio 2015 to build professional apps for Windows 10. However, this is not the end of the story. You have cleared the first hurdle, but the best C# programmers learn from continued experience, and you can gain this experience only by building C# apps. As you do so, you will discover new ways to use the C# language and many features in Visual Studio 2015 that I have not had space to cover in this book. Also, remember that C# is an evolving language. Back in 2001, when I wrote the first edition of this book, C# introduced the syntax and semantics necessary to build apps that made use of Microsoft .NET Framework 1.0. Some enhancements were added to Visual Studio and .NET Framework 1.1 in 2003, and then in 2005, C# 2.0 emerged with support for generics and .NET Framework 2.0. C# 3.0 added numerous features, such as anonymous types, lambda expressions, and, most significantly, LINQ. C# 4.0 extended the language further with support for named arguments, optional parameters, contravariant and covariant interfaces, and integration with dynamic languages. C# 5.0 added full support for asynchronous processing through the async keyword and the await operator. C# 6.0 has provided further tweaks to the language, such as expression-bodied methods, string interpolation, the nameof operator, exception filters, and many others.

In parallel with the evolution of the C# programming language, the Windows operating system has changed considerably since the first edition of this book. Arguably, the changes instigated by Windows 8 onward have been the most radical in this period, and developers familiar with earlier editions of Windows now have exciting new challenges to build apps for the modern, touch-centric, mobile platform that Windows 10 provides. Visual Studio 2015 and C# will undoubtedly be instrumental in assisting you to address these challenges.

What will the next version of C# and Visual Studio bring? Watch this space!

## Quick reference

| To | Do this |
|---|---|
| Create an entity model by using the Entity Framework | Add a new item to your project by using the ADO.NET Entity Data Model template. Use the Entity Data Model Wizard to connect to the database containing the tables that you want to model and select the tables that your app requires. In the data model, remove any columns that are not used by your app (as long as they have default values), if your app is inserting new items into the database. |
| Create a REST web service that provides remote access to a database through an entity model | Create an ASP.NET project using the Web API template. Run the Add Scaffold wizard and select Web API 5 Controller With Read/Write Actions, Using Entity Framework. Specify the name of the appropriate entity class from the entity model as the model class, and the data context class for the entity model as the data context class. |
| Consume a REST web service in a UWP app | Add the ASP.NET Web client libraries to the project and use an HttpClient object to connect to the database. Set the BaseAddress property of the HttpClient object to reference the address of the web service. For example: ``` string ServerUrl = "http://localhost:50000/"; HttpClient client = new HttpClient(); client.BaseAddress = new Uri(ServerUrl); ``` |
| Retrieve data from a REST web service in a UWP app | Call the GetAsync method of the HttpClient object and specify the URI of the resource to access. If the GetAsync method is successful, fetch the data by using the ReadAsStringAsync method of the HttpResponseMessage object returned by the GetAsync method. For example: ``` HttpClient client = ...; var response = await client.GetAsync("api/customers"); if (response.IsSuccessStatusCode) { var customerData = await response.Content. ReadAsStringAsync(); ... } else { // GET failed } ``` |
| Add a new data item to a REST web service from a UWP app | Use the PostAsync method of the HttpClient object and specify the new item to create and the URI of the collection to hold this item as parameters. Examine the status of the HttpResponseMessage object returned by PostAsync to verify that the POST operation succeeded. For example: ``` HttpClient client = ...; StringContent newCustomer = ...; var response = await client.PostAsync( "api/customers", newCustomer); if (!response.IsSuccessStatusCode) { // POST failed } ``` |

## Update an existing item in a REST web service from a UWP app

Use the PutAsync method of the HttpClient object and specify the item to update and the URL of this item as parameters. Examine the status of the HttpResponseMessage object returned by PutAsync to verify that the PUT operation succeeded. For example:

```
HttpClient client = ...;
StringContent updatedCustomer = ...;
string path =
    "$"api/customers/{updatedCustomer.CustomerID}";
var response = await client.PutAsync(
    path, updatedCustomer);
if (!response.IsSuccessStatusCode)
{
    // PUT failed
}
```

## Index

## Symbols

+   - & (ampersand)
+     - & (AND) operator, 354
+     - && (logical AND) operator, 89–90, 105
+   - <> (angle brackets)
+     - => operator, 62
+     - => operator in lambda expressions, 413
+     - > (greater than) operator, 89
+     - >= (greater than or equal to) operator, 89
+     - < (less than) operator, 89
+     - <= (less than or equal to) operator, 89
+   - * (asterisk), 11, 45, 198, 504
+   - @ (at symbol), 178
+   - \ (backslash), 104
+   - { } (braces or curly brackets), 53, 60
+   - : (colon), 79
+   - $ (dollar sign), 46
+   - = (equal sign), 37, 53–54, 91
+     - == (equal to) operator, 88–89, 505
+     - associativity and, 53–54
+   - ! (exclamation point)
+     - != (inequality) operator, 505
+     - ! (NOT operator), 88
+   - / (forward slash), 11, 45, 504
+   - - (minus sign), 45, 503–504
+     - -= (compound subtraction) operator, 108, 125
+     - -- (decrement) operator, 55
+     - -= (subtraction and assignment) operator, 457
+   - () (parentheses), 53, 60, 413
+     - in Boolean expressions, 92
+     - in expressions, 89
+     - in method calls, 64, 66
+     - precedence override, 90
+   - | (pipe symbol)
+     - | (OR) operator, 354
