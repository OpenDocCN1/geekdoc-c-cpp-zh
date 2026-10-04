# VB.NET

Try

```
Dim myMessage As New MailMessage()
...
System.Threading.Thread.Sleep(5000)
Catch ex As SmtpException
    Message.Text = "An error occurred while sending your e-mail. Please try again."
Finally
    Message.Visible = True
End Try
```

# C#

```
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

# How It Works

When an exception occurs at runtime, .NET checks if it is wrapped in a Try Catch block. If that's the case, it scans the list of Catch blocks for an Exception type that matches the exception being thrown. Only the first Catch block that matches the Exception is being called; all remaining Catch blocks are ignored. Code in the Try block following the line that caused the exception is not executed anymore.

In this exercise, the code has a Catch block for the SmtpException type, which is executed when an exception of that type—or of its subtypes—is encountered. As you learned before, you can have multiple Catch blocks, each dealing with a specific type of exception. All other exceptions won't be handled by this code. You see how to deal with these exceptions in a later section.

With these Try Catch blocks, you can write code that deals with errors that you think might happen in your code. It's always a good practice to wrap code that might throw an error in a Try Catch block so you can deal with it gracefully. Some examples of code that might throw an exception include: