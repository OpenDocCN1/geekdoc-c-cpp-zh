
VB.NET

```
Imports System.Net.Mail
```

C#

```
using System.Net.Mail;
```

- 3. Add the following code to a Page_Load handler. If you're using VB.NET, you need to set up the handler first using the two drop-down lists at the top of the Document Window (or by double-clicking the page in Design View):

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Dim myMessage As MailMessage = New MailMessage()
    myMessage.Subject = "Test Message"
    myMessage.Body = "Hello world, from Planet Wrox"
    myMessage.From = New MailAddress("you@example.com", "Sender Name")
    myMessage.To.Add(New MailAddress("you@example.com", "Receiver Name"))

    Dim mySmtpClient As SmtpClient = New SmtpClient()
    mySmtpClient.Send(myMessage)
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    MailMessage myMessage = new MailMessage();
    myMessage.Subject = "Test Message";
    myMessage.Body = "Hello world, from Planet Wrox";
    myMessage.From = new MailAddress("you@example.com", "Sender Name");
    myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));

    SmtpClient mySmtpClient = new SmtpClient();
    mySmtpClient.Send(myMessage);
}
```

Change the e-mail addresses and names in the two lines that set the From and To addresses to your own. If you have only one e-mail address, you can use the same address for the sender and the receiver.

- 4. Open Web.config and right before the closing </configuration> tag, add the following settings:

```
<system.net>
  <mailSettings>
    <smtp deliveryMethod="Network" from="Your Name &lt;you@example.com&gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
</configuration>
```

Don't forget to change smtp.example.com to the name of your SMTP server. Also, be sure to enter your name and e-mail address in the from attribute. If necessary, add the userName, password, enableSsl, and port attributes to the <network> element as shown earlier.

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

The ReadAllText method is useful to read the complete contents of a text file. For example, when sending text by e-mail, you could store the body text of the e-mail in a text file. When you're about to send the e-mail, you call ReadAllText and assign the contents that this method returns to the body of the e-mail. You see how this works in the following Try It Out.

## TRY IT OUT Sending Mail from the ContactForm User Control

This exercise shows you how to use e-mail to send the user data from the contact form to your own Inbox. As the body of the e-mail message, the code reads in a text file that contains placeholders. These placeholders are filled with the actual user data from the form.

- 1. Start by adding a new text file to the App_Data folder in your website. If you don't have the App_Data folder yet, right-click the website and choose Add ▸ Add ASP.NET Folder ▸ App_Data. Create the text file by right-clicking the App_Data folder and choosing Add ▸ Add New Item. Then select Text File, name the file ContactForm.txt, and click Add.
- 2. Enter the following text in the text file, including the placeholders wrapped in a pair of double hash symbols:
- 3. Open the Code Behind of the ContactForm.ascx user control and import the following namespaces (no need to type the comments) at the top of the file:
- 4. Switch to Markup View and add runat="server" and id="FormTable" attributes to the table with the server controls. This way you can hide the entire table programmatically when the form has been submitted. To do this, locate the opening <table> tag and modify it like this:

```
Hi there,

A user has left the following feedback at the site:

Name: ##Name##
E-mail address: ##Email##
Home phone: ##HomePhone##
Business phone: ##BusinessPhone##
Comments: ##Comments##
```

Save and close the file.

```
VB.NET
Imports System.IO ' Provides access to the File class for reading the file
Imports System.Net.Mail ' Provides access to the various mail related classes

Partial Class Controls_ContactForm
Inherits System.Web.UI.UserControl
```

```
C#
using System.IO; // Provides access to the File class for reading the file
using System.Net.Mail; // Provides access to the various mail related classes

public partial class Controls_ContactForm : System.Web.UI.UserControl
```

```
<table class="auto-style1" runat="server" id="FormTable">
```

```
MailMessage myMessage = new MailMessage();
myMessage.Subject = "Response from web site";
myMessage.Body = mailBody;

myMessage.From = new MailAddress("you@example.com", "Sender Name");
myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));
myMessage.ReplyToList.Add(new MailAddress(EmailAddress.Text));

SmtpClient mySmtpClient = new SmtpClient();
mySmtpClient.Send(myMessage);

Message.Visible = true;
FormTable.Visible = false;
}
```

Again, make sure you replace the e-mail addresses for the From and To properties of the MailMessage with your own. Also, the replace method is case sensitive so make sure you type the placeholders exactly as how you wrote them in the text file.

- 7. Save all your changes and once again request the Contact.aspx page in the browser. Enter your details and click the Send button. You'll see the text Message Sent appear.
- 8. Check the e-mail account you sent the e-mail to (or look in the folder C:\TempMail if you're dropping your mail on disk) and you should see an e-mail message similar to Figure 9-11.

![](img/eadab2ccd79b253c01a3fdff2321202d_388_0.png)

## FIGURE 9-11

## How It Works

The mail-sending part of this exercise is pretty similar to the demo page you created earlier. What’s different, however, is where the body text for the mail message comes from. Instead of hard-coding the body in the Code Behind of the ContactForm control, you moved the text to a separate file. This file in turn contains a few placeholders that are replaced at run time with the user’s details. To read in the entire file at once, you use the following code:

```
VB.NET
Dim fileName As String = Server.MapPath("~/App_Data/ContactForm.txt")
Dim mailBody As String = File.ReadAllText(fileName)
```

```
C#
string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
string mailBody = File.ReadAllText(fileName);
```

The first line uses Server.MapPath to translate a virtual path into its physical counterpart. By using the virtual path, it’s easier to move your site to a different location because it doesn’t depend on any hard-coded paths. Server.MapPath("~/App_Data/ContactForm.txt") returns a physical path such as C:\BegASPNET\Site\App_Data\ContactForm.txt. This path is then fed to the ReadAllText method of the File class, which opens the file and returns its contents, which are then assigned to the mailBody variable.

> NOTE Reading this file every time you need it isn’t very efficient. In Chapter 15, you see how to cache the contents of this file so you don’t have to read it on every request.

The code then uses a number of calls to the Replace method of the String class to replace the static placeholders in the message body with the details the user entered in the contact form. The return value of the Replace method—the new text with the replaced strings—is reassigned to the mailBody variable. After the final call to Replace, the mailBody no longer contains the placeholders, but the user’s details instead:

```
VB.NET
mailBody = mailBody.Replace("##Name##", Name.Text)
...
mailBody = mailBody.Replace("##Comments##", Comments.Text)
```

```
C#
mailBody = mailBody.Replace("##Name##", Name.Text);
...
mailBody = mailBody.Replace("##Comments##", Comments.Text);
```

The Replace method is case sensitive, so if you find that some placeholders are not replaced correctly, make sure you used the same capitalization in the code and in the message body.

The placeholders are wrapped in a pair of double hash symbols (##). The hash symbols are arbitrarily chosen, but help to identify the placeholders, minimizing the risk that you accidentally replace some text that is supposed to be in the actual message.
