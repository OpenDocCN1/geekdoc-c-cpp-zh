and type ''' (three tick characters) for VB or /// (three forward slashes) for C#. As soon as you do that, the IDE inserts XML tags for the summary and, optionally, the parameters and return type of a method. Once again, consider a SendEmailMessage method. It could have two parameters of type String: one for the e-mail address to send the message to, and one for the mail body. With the XML comments applied, the method could look like this:

# VB.NET

```
```vb
''' <summary>
''' Sends out an e-mail to the address specified by emailAddress.
''' </summary>
''' <param name="emailAddress">The e-mail address of the recipient.</param>
''' <param name="mailBody">The body of the mail message.</param>
''' <returns>This method returns True when the message was sent successfully;
''' and False otherwise.</returns>
''' <remarks>Attention: this method assumes a valid mail server is
''' available.</remarks>
Public Function SendEmailMessage(emailAddress As String,
    mailBody As String) As Boolean
    ' Implementation goes here
End Function
```
```

# C#

```
```csharp
// <summary>
// Sends out an e-mail to the address specified by emailAddress.
// </summary>
// <param name="emailAddress">The e-mail address of the recipient.</param>
// <param name="mailBody">The body of the mail message.</param>
// <returns>This method returns true when the message was sent successfully;
// and false otherwise.</returns>
// <remarks>Attention: this method assumes a valid mail server is
// available.</remarks>
public bool SendEmailMessage(string emailAddress, string mailBody)
{
    // Implementation goes here
}
```
```

The cool thing about this type of commenting is that the comments you type here show up in IntelliSense in the code editor when you try to call the method (see Figure 5-6).

![](bbox=[0.18, 0.86, 0.55, 0.92])

# FIGURE 5-6

This makes it much easier for you and other developers to understand the purpose of the method and its parameters.

In addition to aiding development in the code editor, you can also use the XML comments to create good-looking, MSDN-like documentation. A number of third-party tools are available that help you with this, including Microsoft's own Sandcastle (http://msdn.microsoft.com/en-us/vstudio/bb608422.aspx) and Document! X from Innovasys (www.innovasys.com/).