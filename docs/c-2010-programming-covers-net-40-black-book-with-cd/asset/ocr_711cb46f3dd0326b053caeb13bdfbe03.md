As shown in Figure 36.7, anonymous authentication is enabled by default in IIS 7.5. When a user requests for an ASP.NET application, the IIS recognizes the user as an anonymous user. The authentication then passes on to the ASP.NET application. You can also make an ASP.NET application to use anonymous authentication to authenticate users. To do so, you need to use the <authentication> element in the web.config file of the application, as given in the following code:

```
<authentication mode="None" />
```

You can find more information about the <authentication> element in the web.config file later in this chapter.

In IIS, an anonymous user is represented by the IUSR account, which is a built-in account with very less privileges to access the ASP.NET applications. Note that the IUSR substitutes the IUSR_<ComputerName> account, for example, IUSR_AVANTIKA-PC, where AVANTIKA-PC is the name of the computer. The IUSR_<ComputerName> account is also present in IIS 7.5, but is used only for File Transfer Protocol (FTP) applications. If you have not installed the FTP server, then this account does not exist.

If you access the applicationHost.config file in the C:\Windows\System32\inetsrv\config folder on your computer, you can see that the IUSR account is used for anonymous access, as shown in the following code:

```
<anonymousAuthentication enabled="true" userName="IUSR" />
```

The <anonymousAuthentication> element is a child element of the <authentication> element in the applicationHost.config file.

You can make changes in the applicationHost.config file or IIS Manager to process Anonymous authentication under a user account other than the default IUSR account. For this, you can right-click the Anonymous Authentication option in IIS Manager and select the Edit option. The Edit Anonymous Authentication Credentials dialog box appears, as shown in Figure 36.8:

![](bbox=[0.195, 0.42, 0.735, 0.625])

Figure 36.8: Editing the Account for Anonymous Authentication

Now, click the Set button on the dialog box. The Set Credentials dialog box opens(Figure 36.9). In this dialog box, you need to enter the details, such as the user name and password.

![](bbox=[0.265, 0.69, 0.67, 0.895])

Figure 36.9: Specifying a Custom User Account for Anonymous Authentication