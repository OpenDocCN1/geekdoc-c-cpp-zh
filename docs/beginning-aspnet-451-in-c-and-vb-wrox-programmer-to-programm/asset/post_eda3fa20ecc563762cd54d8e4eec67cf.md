
myMessage.To.Add(New MailAddress("you@example.com", "Receiver Name"))
myMessage.ReplyToList.Add(New MailAddress(EmailAddress.Text))

```vb
Dim SmtpClient = New SmtpClient
mymtpClient.Send(myMessage)
```

```vb
Message.Visible = True
FormTable.Visible = False
End If
```

## C#

```csharp
protected void SendButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
        string mailBody = File.ReadAllText(fileName);

        mailBody = mailBody.Replace("##Name##", Name.Text);
        mailBody = mailBody.Replace("##EmailAddress##", EmailAddress.Text);
        mailBody = mailBody.Replace("##Phone##", PhoneHome.Text);
        mailBody = mailBody.Replace("##BusinessPhone##", PhoneBusiness.Text);
        mailBody = mailBody.Replace("##Comments##", Comments.Text);

        myMessage = new MailMessage();
        myMessage.Subject = "Response from web site";
        myMessage.Body = mailBody;

        myMessage.From = new MailAddress("you@example.com", "Sender Name");
        myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));
        myMessage.ReplyToList.Add(new MailAddress(EmailAddress.Text));

        smtpClient = new SmtpClient();
        mySmtpClient.Send(myMessage);

        Message.Visible = true;
        FormTable.Visible = false;
    }
}
```

Again, make sure you replace the e-mail addresses for the From and To properties of the Message with your own. Also, the replace method is case sensitive so make sure you type the placeholders exactly how you wrote them in the text.

- 7. Save all your changes and once again request the Contact.aspx page in the browser. Enter your details and click the Send button. You will see the text Message appear.

- 8. Check the e-mail you sent to yourself (or in the folder C:\TempMail if you're dropping your mail on disk) and you will see an e-mail similar to Figure 9-11.

## Processing Data at the Server | 331

![](img/9e033e3b9560597824f8b22941d6d8bb_368_0.png)

## How It Works

The mail-sending part of this exercise is pretty similar to the demo page you created earlier. What’s different, however, is where the body text for the mail message comes from. Instead of hard-coding the body in the Code Behind of the FormControl control, you moved the text to a separate file. This file contains few placeholders that are replaced at run with the user’s details. To read the entire file in one, use the following code:

## VBNET

```vb
Dim fileName As String = Server.MapPath("/App_Data/ContactForm.txt")
Dim mailBody As String = File.ReadAllText(fileName)
```

## C#

```csharp
string fileName = Server.MapPath("/App_Data/ContactForm.txt")
string mailBody = File.ReadAllText(fileName);
```

The first lines use Server.MapPath to translate a virtual path into its physical counterpart because it doesn't depend on any hard-coded paths. By using the virtual path, it's easier to move your site to a different location because Server.MapPath("/App_Data/ContactForm.txt") returns a physical path such as C:\BegASPNET\Site\App_Data\ContactForm.txt. This path is then found to the ReadAllText method of the File class, which opens the file and returns its contents, which are then assigned to the mail-Body variable.

## CHAPTER 9 VALIDATING USER INPUT

> NOTE: Reading this file every time you need it isn't very efficient. In Chapter 15 you will see how to cache the contents of a file so you don't have to read it on every request.

The code uses a number of calls to the Replace method of the String class to replace the static placeholders in the mail body with the user entered in the contact form. The return value of the Replace method — the new text with the replaced strings — is reassigned to the mailBody variable. After the final call to Replace, the mailBody no longer contains placeholders, but the user's details include:

```vb
VB.NET
mailBody = mailBody.Replace("##Name##", Name.Text)
mailBody = mailBody.Replace("##Comments##", Comments.Text)

// C#
mailBody = mailBody.Replace("##Name##", Name.Text);
mailBody = mailBody.Replace("##Comments##", Comments.Text);
```

The Replace method is case sensitive, if you find that placeholders are not replaced correctly, make sure you use the same capitalization in the code and in the message body.

The placeholders are wrapped in a pair of double hash symbols (##). The hash symbols are arbitrarily chosen, help to identify the placeholders, minimizing the risk that you accidentally replace text that is supposed to be in the actual message.

Once the message body is set up, it's assigned to the Body property of the MailMessage object, which is then sent using the SmtpClient, identical to what you see in an earlier exercise.

You may have noticed the call to the ReplyTo collection of the MailMessage instance. This code adds the e-mail address that the user entered in the EmailAddress box to the reply-to list of the mail body. This means that when you receive the message and want to reply to it, the reply gets to the user's address instead of the From address you assigned to the message. This is especially useful in contact forms where users enter an e-mail address so you can directly reply to them. You may be tempted to assign the address the user entered to the From property directly, but are advised not to do this. Some mail servers require this to be your own and thus sending the mail may fail. Your message may be rejected when users enter an invalid address. By setting the From address to one of your own and adding the user's address to the ReplyToList, you create a reliable, yet convenient solution.

When you filled in your details in the contact form and clicked the Send button, you may have noticed some page flicker as the page submits to the server and is reloaded with the success message. This page flicker can easily be minimized or completely removed using Ajax technologies, which are discussed in the next chapter.

## PRACTICAL TIPS ON VALIDATING DATA

The following list provides practical tips on validating data:

- Always validate all user input. Whenever you have a public website on the Internet, you lose the control to it. To stop malicious users from entering bogus data in your system, always validate your users using the ASP.NET validation controls.

- Always provide useful error messages in your validation controls. Assign the error message to the ErrorMessage property and leave the Text empty, or use a ValidationSummary control to show a list of error messages.

- Consider using the CssClass attribute of the validation controls to move the style definitions for the error messages to a separate CSS file instead of setting directly on the validation controls.

- Whenever you are writing code that sends an e-mail, moving the body of the e-mail to a separate text file stored in the App_Data folder because it makes your application much easier to maintain.

- When storing data in XML files, store them in the App_Data folder that is designed specifically for this purpose. By way, all your data files are nicely packed together. More, by default the web server connects these to the files so a visitor to your site cannot request them directly.

- When sending emails as a test, always send to an existing and valid address. Even though an address like asdf@test.com may appear to be invalid, there's a fair chance the account exists and is monitored, leading to the possibility of losing sensitive data, like passwords you may be sending through e-mail.

- Consider using SpecifiedPickupDirectory as the DeliveryMethod for SMTP mail during development. It avoids the need to send messages over the network, resulting in a faster response and a cleaner inbox.

## SUMMARY

User input is an important aspect of most interactive websites. The input comes from different sources in your website: the contact form you created in this chapter, the query string, and other sources. To stop users from entering invalid or even dangerous content into your system, it's important to validate all input before you work with it.

The biggest benefit of the validation controls that ship with ASP.NET is that they work at the client and at the server, enabling you to create responsive forms where users get immediate feedback about any errors they make, without the need for a full postback. At the same time, the data is validated at the server, ensuring that data coming from clients JavaScript is valid as well.

To store the information that users submit to your site, you have a couple of options. The data can be stored in a database or a text file or sent by e-mail. The latter option is particularly useful for contact forms, so you get an immediate alert when someone leaves a comment at your website.
