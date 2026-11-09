![](bbox=[0.211, 0.136, 0.494, 0.311])

Fig.ASP-5.41

![](bbox=[0.527, 0.136, 0.813, 0.311])

Fig.ASP-5.42

Now, let’s learn how to configure the virtual SMTP e-mail server using the web.config file for password recovery after learning about the PasswordRecovery control.

# Configuring the web.config File for Password Recovery

While using the PasswordRecovery control, you need to specify the mail server settings in the **web.config** file of your application to receive your password on your e-mail id. The configuration file contains the `<system.net>` XML tag element. This element has e-mail configurations defined in its child element `<mailSettings>` tag. As SMTP is the network standard followed by ASP.NET Web applications to transmit e-mails, the user’s e-mail is recognized in the `<smtp...>` `</smtp>` XML element tags.

The code snippet of the `<system.net>` XML tag of the **web.config** file is as follows:

```
```xml
<system.net>
    <mailSettings>
        <smtp from="puneet.saxena@kogentindia.com">
            <network host="smtpout.seruter.net" password="puneet"
userName="puneet.saxena@kogentindia.com" />
        </smtp>
    </mailSettings>
</system.net>
```
```

In the preceding code snippet, the `<smtp>` element has an attribute **from** which specifies the e-mail id from which the e-mail is sent that contains the retrieved password. The `<smtp>` element also contains a subelement, known as `<network>`. The `<network>` subelement has the following attributes:

+   - **host:** Contains the value of the host server
+   - **password:** Contains the password of the e-mail account from which the e-mail is sent
+   - **userName:** Contains the e-mail id of the user from which the e-mail is sent

# Summary

This chapter discusses various Login controls available in ASP.NET 4.0, such as Login, LoginView, PasswordRecovery, LoginStatus, LoginName, and ChangePassword. You have also learned how to implement these controls and how to create a user account in ASP.NET by using the **ASP.NET Web Site Administration Tool**. The chapter also discusses the noteworthy properties and methods of all these controls.

In the next chapter, you will learn about ADO.NET and its architecture. In addition to that you will also learn about various datasource and databound controls, such as SqlDataSource, AccessDataSource, GridView, DataList, and DetailsView.