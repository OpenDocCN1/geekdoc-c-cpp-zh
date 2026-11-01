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

+   7. Save all your changes and once again request the Contact.aspx page in the browser. Enter your details and click the Send button. You'll see the text Message Sent appear.
+   
+   8. Check the e-mail account you sent the e-mail to (or look in the folder C:\TempMail if you're dropping your mail on disk) and you should see an e-mail message similar to Figure 9-11.

![](bbox=[0.2, 0.6, 0.85, 0.92])

# FIGURE 9-11