| Control/Data Type | Prefix | Example |
|---|---|---|
| Type: Double | d | dGrossPay |
| Type: Currency | c | cNetSales |
| Type: Date | dt | dtHired |
| Type: Object | o | oControl |
| Type: String | s | sLastName |
| Type: Variant | v | vCompany |
| Scope: Local | None | sState |
| Scope: Private | m | msState |
| Scope: Public | g | gsState |

One benefit to using shorter prefixes for variables and longer prefixes for controls is that it becomes easy to tell them apart when you're reading your code. Also note that more commonly used data types get the one-character prefixes. You'll typically use Booleans more often than Bytes, so a shorter prefix for Booleans saves typing.

Some developers don't use any prefixes for variables. There's nothing wrong with that. There are some advantages to using prefixes, however. The first advantage is that you can identify the data type at the point you're using the variable. It's easy to see that a statement like sCustomer = chkActive may cause a problem. You know sCustomer is a String data type, and chkActive, being a check box control, returns a Boolean value. Another advantage is variable name uniqueness. Recall that the variable naming rules state that all variable names must be unique and that you can't use reserved keywords for variable names. That means that you can't have a Boolean variable named Print that determines whether to print a report. By using a prefix, bPrint does not violate any rules.

Including an additional prefix for the scope conveys similar advantages. Knowing the scope of the variable in the portion of code you're working helps debug the code when things go wrong. It also allows you to use similar variables with different scopes. For example, you could have a private module-level variable mbIsEnabled that applies to all the code in your module and still have a local procedure-level variable bIsEnabled for use in only that procedure.

One final advantage to a naming convention that uses a mix of uppercase and lowercase letters is that you can detect spelling errors in your variable names very quickly. VBA will change the case of the variable name to match the case you use when you declare it. If you declare a variable using Dim sFirstName As String and later type sfirstname = "Larry" (all lowercase), as soon as you complete that line of code, your variable will change to sFirstName = "Larry". That immediate feedback will help you catch spelling errors before they become problems.