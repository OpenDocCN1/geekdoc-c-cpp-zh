# How to use the PasswordRecovery control

It’s inevitable that some users will forget their passwords. Fortunately, the PasswordRecovery control makes it easy to automate the process of recovering forgotten passwords. This process is described in figure 19-12, and it’s especially useful if you are managing a site with a large number of users.

When you use the PasswordRecovery control, the password is sent to the user via email. As a result, you need to make sure that your system is set up so it can send email before you test this control. By default, an application will try to send email to an SMTP server set to localhost on port 25.

The most important element of the PasswordRecovery control is the MailDefinition element. In particular, you must set the From attribute of the MailDefinition element to the email address that’s sending the email message or an error will occur when your system attempts to send the email. Typically, the From email address is set to the email address that’s used by the web site administrator. If you set this attribute correctly, a standard message will be sent to the user. To customize the subject line and message body, you can edit the other attributes of the MailDefinition element.

The PasswordRecovery control uses three views. In the Web Forms Designer, you can switch between these three views by using the smart tag menu, and you can edit the properties for any of these views as necessary.

When you display this control in a browser, the first view asks the user to enter a user name. Then, the second view requires the user to answer the security question. If the answer to this question is correct, the password is emailed to the address that’s associated with the user name, and the third view is displayed. This view displays a message that indicates that the password recovery was successful and that the password has been sent to the user via email.