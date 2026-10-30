convert any numeric variables to string before assigning their value. In the following example, Session("DiscountTotal") is a session variable and DiscountTotalDecimal is a module-level variable.

```
' Declare a module-level variable
Private DiscountTotalDecimal As Decimal

Private Sub SubmitButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles SubmitButton.Click
' Perform calculations.
Dim DiscountDecimal As Decimal
' Omitted code to convert input to numeric and calculate a discount.
' Add to the discount total.
DiscountTotalDecimal += DiscountDecimal
' Save the discount total in a session variable.
Session("DiscountTotal") = DiscountTotalDecimal.ToString()
End Sub
```

# Checking for Postback

When an ASP.NET Web application loads, the Page_Load event occurs. But unlike Windows applications, the page is reloaded for each "round-trip" to the server (each postback). Therefore, the Page_Load event occurs many times in a Web application. The page's IsPostBack property is set to false for the initial page load and to true for all page loads following the first. If you want to perform an initialization task once, you can test for IsPostBack = False (or Not IsPostBack) in the Page_Load event handler. And if you want to make sure that you perform an action only on postback (not the initial page load), you can check for IsPostBack = True.

```
Private Sub Page_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles MyBase.Load
' If a value exists for the discount total, ...
If IsPostBack And (Session("DiscountTotal") IsNot Nothing) Then
DiscountTotalDecimal = Decimal.Parse(Session("DiscountTotal").ToString)
End If
```

Notice that the module-level variable, DiscountTotalDecimal, is assigned a value only on postback and if the session variable already has been assigned a value.

# Feedback 7.4

+   1. Write the statement to store the value in EmailTextBox to a Session object in a variable called Email.
+   2. What code is required to retrieve the value stored in the Session object Email and assign it to EmailLabel?
+   3. Write the code to send the Email value to a cookie on the client machine. Give the cookie an expiration of three years.
+   4. What technique(s) for state management allows you to share the values with other Web pages in the same application or session?