If you can't make sending mails from your local machine work, you can always use the SpecifiedPickupDirectory delivery option to store the files on your local machine. This way, you need to configure the mail server when you deploy your website, and it gives you a quick, convenient solution during development.

# How It Works

You added the following Imports or using statement to the Code behind:

```
VB.NET

Imports System.Net.Mail

C#
\using System.Net.Mail;
```

This statement is used to make the classes in this namespace available in your code without prefixing them with their full namespace. This enables you, for example, to create a MailMessage instance like this:

```
VB.NET
myMessage As MailMessage = New MailMessage()

C#
MailMessage myMessage = new MailMessage();
```

Without the Imports or using statement, you would need this code instead:

```
VB.NET
myMessage As System.Net.Mail.MailMessage = New System.Net.Mail.MailMessage()

C#nSystem.Net.Mail.MailMessage myMessage = new System.Net.Mail.MailMessage();
```

The code in Page_Load creates a new MailMessage object and sets its Subject and Body properties. The code then addresses for the sender and recipient of the e-mail message:

```
VB.NET
myMessage.From = New MailAddress("*@example.com", "Sender Name")
myMessage.To.Add(new MailAddress("*@example.com", "Receiver Name"));

C#nmyMessage.From = new MailAddress("*@example.com", "Sender Name")
myMessage.To.Add(new MailAddress("*@example.com", "Receiver Name"));
```

The From property of the MailMessage is of type MailAddress, so you can assign a new MailAddress directly. The constructor of the MailAddress class accepts the e-mail address and friendly name as strings, so you can create and assign the From address with a single line of code.