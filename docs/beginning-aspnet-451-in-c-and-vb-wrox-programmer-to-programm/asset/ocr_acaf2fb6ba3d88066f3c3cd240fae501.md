# VB.NET

```
Dim userMessage As String = String.Empty
Try
mySmtpClient.Send(myMessage)
Message = "Message sent"
Catch ex As Exception
Message = "An unknown error occurred."
Finally
Message.Text = userMessage
End Try
```

# C#

```
string userMessage = string.Empty;
try{
  mySmtpClient.Send(myMessage);
  userMessage = "Message sent";
} catch (Exception ex){
  userMessage = "An unknown error occurred.";
} finally {
  Message.Text = userMessage;
}
```

In this code example, the Catch block is set up to handle an exception of type System.Exception, the base class of all exceptions in the .NET Framework. This exception is sent by. In C#, you could leave out the ex variable if you don't use it in your code:

# C#

```
catch (Exception)
{
  userMessage = "An unknown error occurred.";
}
```

The ability to specify an Exception type is useful when you think your code can encounter more than one exception. In that case, you can have multiple Catch blocks for different Exception types. The following code is capable of handling a specific SmtpException that may occur during the mail sending operation, and it's also capable of catching all other exceptions using its generic Catch block:

# VB.NET

```
Try
  mySmtpClient.Send(myMessage)
Catch smtpException As SmtpException
  userMessage = "Sorry, an error occurred while sending your message."
Catch ex As Exception
  ' Something else went wrong.\nEnd Try
```