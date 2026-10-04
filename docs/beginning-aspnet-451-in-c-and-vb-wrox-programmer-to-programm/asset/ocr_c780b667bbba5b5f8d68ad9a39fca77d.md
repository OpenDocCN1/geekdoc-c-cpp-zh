+   4. Save all your changes and request `SignUp.aspx` in the browser.
5. Fill in the form, but for both password fields, type something short like pass.
6. Click the Create User button. Note that the control now forces you to enter a password with a minimum length of seven characters that contains at least one non-alphanumeric character. It displays an appropriate error message below the control, shown in Figure 16-15. Note that numbers are not considered non-alphanumeric characters, so you need to make sure your password contains at least one character like # or $ or *. For example, `Pa55word` is not a valid password, but `Pass##Word` will be accepted. Also note that the password is case sensitive.
7. Enter a password of at least seven characters with at least one non-alphanumeric character like # or $ and click the Create User button again. This time your password is accepted and the account is created.

![](bbox=[0.53, 0.13, 0.88, 0.24])

FIGURE 16-15

# How It Works

The `CreateUserWizard` uses the configured Membership provider under the hood to validate the data and create the user. The provider in turn consults the `Web.config` file for the configuration information such as the minimum password length. When you try to create the user, the provider enforces the rules set in `Web.config` and cancels the user creation process as soon as one of the rules is not fulfilled.

Having the configuration information in `Web.config` is especially useful when you deploy your application to a different server that uses a different database, because all you need to do is change the settings in this file. Chapter 19 and Appendix B show you how to do this.

So far, you have seen how to let users sign up for an account so they can log in. But how can you differentiate between the different users in the system? How can you block access to specific folders such as the `Management` folder for unauthorized users? You do this with the Role Manager, another application service that ships with ASP.NET.

# THE ROLE MANAGER

Although it’s nice that your users can now sign up and log in to your site, it would be a lot more useful if you could differentiate among your users. That would enable you to grant access rights to one or just a few users to access the `Management` folder so only they can change your reviews and genres. With the Role Manager that ships with ASP.NET, this is pretty easy to do. The Role Manager enables you to assign users to different roles. You can then use these roles to open or block specific functionality in your site. For example, you can block access to the `Management` folder for all users except for those in the Managers role. Additionally, you can display different content based on the roles users have with the `LoginView` as you saw earlier.