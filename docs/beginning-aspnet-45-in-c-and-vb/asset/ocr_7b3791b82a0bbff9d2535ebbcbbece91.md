This statement is used to make the classes in this namespace available in your code without prefixing them with their full namespace. This enables you, for example, to create a MailMessage instance like this:

```
VB.NET
Dim myMessage As MailMessage = New MailMessage()
```

```
C#
MailMessage myMessage = new MailMessage();
```

Without the Imports or using statement, you would need this longer code instead:

```
VB.NET
Dim myMessage As System.Net.Mail.MailMessage = New System.Net.Mail.MailMessage()
```

```
C#
System.Net.Mail.MailMessage myMessage = new System.Net.Mail.MailMessage();
```

The code in Page_Load creates a new MailMessage object and sets its Subject and Body properties. The code then assigns addresses for the sender and recipient of the e-mail message:

```
VB.NET
myMessage.From = New MailAddress("you@example.com", "Sender Name")
myMessage.To.Add(New MailAddress("you@example.com", "Receiver Name"))
```

```
C#
myMessage.From = new MailAddress("you@example.com", "Sender Name");
myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));
```

The From property of the MailMessage is of type MailAddress, so you can assign a new MailAddress directly. The constructor of the MailAddress class accepts the e-mail address and friendly name as strings, so you can create and assign the From address with a single line of code.

The To property of the MailMessage class is a collection, so you cannot assign a MailAddress instance directly. Instead, you need to use the Add method to assign an address. This also enables you to add multiple recipients by calling To.Add multiple times, each time passing in a different MailAddress instance. You use the CC and Bcc properties in a similar way to assign e-mail addresses to the carbon copy and blind carbon copy fields of an e-mail message.

The final two lines of the code send out the actual message:

```
VB.NET
Dim mySmtpClient As SmtpClient = New SmtpClient()
mySmtpClient.Send(myMessage)
```

```
C#
SmtpClient mySmtpClient = new SmtpClient();
mySmtpClient.Send(myMessage);
```

When the Send method is called, the SmtpClient scans the Web.config file for a configured SMTP server or local drop folder. It then contacts that server and delivers the message or saves it locally.