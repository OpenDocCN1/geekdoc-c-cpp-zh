
# Exception Handling

configuration above used which in turn off the SmtpClient Save changes to deliver the e-mail at the DoesNotExist which will obviously fail. To save the changes to the file, keep it open so you can easily undo this in a later step.

- 6. Switch back to ExceptionHandling.aspx and press Ctrl+F5 to open up the page in your browser. You should see the "Yellow Screen of Death" with an error message. Scroll down the page to see the Stack Trace, shown in Figure 18-2.

![](img/9e033e3b9560597824f8b22941d6d8bb_708_0.png)

```
[Exception: The name could not be resolved: "DoesNotExist"]
System.Net.Mail.PooledStream.GetConnection(PooledStream, Object object, Boolean object, IPAddress&address, So
System.Net.Mail.PooledStream.Activate(object object, GeneralAsyncdelegate async_callback) +300
System.Net.Mail.PooledStream.Activate(object object, GeneralAsyncdelegate async_callback) +19
System.Net.Mail.PooledStream.GetConnection(ServicePoint servicePoint, Int32 creationTime) +65
System.Net.Mail.PooledStream.GetConnection(ServicePoint servicePoint) +170
System.Net.Mail.PooledStream.Send(MailMessage) +1554
[Exception: The name could not be resolved: "DoesNotExist"]
System.Net.Mail.SmtpClient.Send(MailMessage) +1960
Demo.Page_Load(Object sender, EventArgs e) in c:\DefaultSite\ExceptionHandling.aspx.cs:2
System.Web.UI.Control.OnLoad(object sender, EventArgs e) +51
System.Web.UI.Page.ProcessRequest(Boolean includeStagesBeforeAsync, Boolean includeStagesAfterAsyncPoint) + -
```

Note that two exceptions are listed: a WebException (to indicate that the name DoesNotExist could not be resolved) and a SmtpException. In the SmtpClient encountered and caught the WebException, wrapped in a new SmtpException and threw exception to indicate the type of error that you are.

- 7. Go back to VS and catch the code that assigns the addresses and sends the message in a Try block:

## VB.NET

```vb
Try
    message.From = New MailAddress("*@*example.com")
    message.To.Add(New MailAddress("*@*example.com"))
    Dim SmtpClient As New SmtpClient("DoesNotExist")
    SmtpClient.Send(message)
    message.Text = "Message sent"
Catch ex As SmtpException
    message.Text = "An error occurred while sending your e-mail. Please try again."
End Try
```

## C#

```csharp
try
{
    message.From = new MailAddress("*@*example.com");
    myMessage.To.Add(new MailAddress("you@example.com"));
    smtpClient mySmtpClient = new SmtpClient("DoesNotExist");
    mySmtpClient.Send(myMessage);
    Message.Text = "Message sent";
}
catch (SmtpException)
{
    Message.Text = "An error occurred while sending the e-mail. Please try again.";
}
```

Notice how the code still contains an invalid mail server.

- 8. Save your changes and request the page in your browser again. You should now see a user-friendly error message, visible in Figure 18-3.

![](img/9e033e3b9560597824f8b22941d6d8bb_709_0.png)

FIGURE 18-3

The exception that is thrown is now caught in the Catch block. Instead of replacing it all the technical details of the exception, the user now gets a friendly message explaining that something went wrong.

- 9. Go back to ExceptionHandling.aspx and fix the code for the SmtpClient by removing the server name from the constructor call:

```vb
Dim mySmtpClient As New SmtpClient()
```

```csharp
smtpClient mySmtpClient = new SmtpClient();
```

Also, in Web.config the changes you made by earlier restoring the <system.net> element.

- 10. Save all changes and refresh ExceptionHandling.aspx in your browser again. You'll now get a message indicating that the e-mail was sent successfully.

- 11. Open ContactForm.ascx from the Controls, switch to its Code Behind, and wrap the code that creates and sends the message in the following Try Catch block. Also, move the line that sets the visibility of the Message control to the Finally block:

## VB.NET

```vb
Dim myMessage As New MailMessage()
...
System.Threading.Thread.Sleep(5000)
Catch ex As SmtpException
    Message.Text = "An error occurred while sending your e-mail. Please try again."
Finally
    Message.Visible = True
End Try
```

## C#

```csharp
try {
    MailMessage myMessage = new MailMessage();
    ...
    System.Threading.Thread.Sleep(5000);
} catch (SmtpException) {
    Message.Text = "An error occurred while sending your e-mail. Please try again";
} finally {
    Message.Visible = true;
}
```

Notice how the line sets the Message control's Visible property to True is now in a Finally block. This, the Label is made visible, regardless of whether an error occurred.

From on, whenever an error occurs during the sending of the e-mail, your users will get a normal error instead of the full error detail page .NET displays by default.

## How It Works

When an exception occurs at runtime, .NET checks if it is wrapped in a Try Catch block. If that's the case, it scans the list of Catch blocks for an Exception type that matches the exception being thrown. Only the first Catch block that matches the Exception is being called; all remaining Catch blocks are ignored. Code in the Try block following the line that caused the exception is not executed anymore.

In this exercise, the code has a Catch block for the SmtpException type, which is executed when an exception of that type—or of its subtypes—is encountered. As you learned before, you can have multiple Catch blocks, each dealing with a specific type of exception. All other exceptions won't be handled by this code. You see how to deal with these exceptions in a later section.

With these Try Catch blocks, you can write code that deals with errors that you think might happen in your code. It's always a good practice to wrap code that might throw an error in a Try Catch block so you can deal with it gracefully. Some examples of code that might throw an exception include:

- Sending e-mail—The server may be down, or you may not have the permissions to access it.
- Accessing a database—The server may be down, you may not have permission to access it, you may get an error due to foreign constraint violations as you saw in Chapter 15, and so on.
- Trying to write an uploaded file to disk—The disk may be full, you may not have the necessary permissions to write to disk, or you are providing an invalid filename.

Although Try blocks are great to avoid exceptions from bubbling up to the user interface, you should use them with care, because they come at a cost. A Try Catch block is generally slower than code without, so you shouldn't use a Try Catch for errors.
