myMessage.To.Add (New MailAddress("you@example.com", "Receiver Name")
myMessage.ReplyToList.Add (New MailAddress(EmailAddress.Text))

```
Dim SmtpClient = New SmtpClient
mySpClient.Send(myMessage)
```

```
Message.Visible = True
FormTable.Visible = False
End If
```

# C#

```
protected void SendButton_Click(object sender, EventArgs e)
{
if (Page.IsValid)
{
string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
string mailBody = File.ReadAllText(fileName);

mailBody = mailBody.Replace("##Name##", Name.Text);
-mailBody = mailBody.Replace("##EmailAddress##", EmailAddress.Text);
-mailBody = mailBody.Replace("##Phone##", PhoneHome.Text);
-mailBody = mailBody.Replace("##BusinessPhone##", PhoneBusiness.Text);
-mailBody = mailBody.Replace("##Comments##", Comments.Text);

myMessage = new MailMessage();
myMessage.Subject = "Response from web site";
myMessage.Body = mailBody;

myMessage.From = new MailAddress("you@example.com", "Sender Name");
myMessage.To.Add (new MailAddress("you@example.com", "Receiver Name"));
myMessage.ReplyToList.Add (new MailAddress(EmailAddress.Text));

smtpClient = new SmtpClient();
mySmtpClient.Send(myMessage);

Message.Visible = true;
FormTable.Visible = false;
}
```

Again, make sure you replace the e-mail addresses for the From and To properties of the Message with your own. Also, the replace method is case sensitive so make sure you type the placeholders exactly how you wrote them in the text.

+   7. Save all your changes and once again request the Contact.aspx page in the browser. Enter your details and click the Send button. You will see the text Message appear.

+   8. Check the e-mail you sent to yourself (or in the folder C:\TempMail if you're dropping your mail on disk) and you will see an e-mail similar to Figure 9-11.