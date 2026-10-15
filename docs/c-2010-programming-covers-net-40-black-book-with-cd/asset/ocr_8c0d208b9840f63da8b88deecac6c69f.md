![](bbox=[0.23, 0.06, 0.84, 0.37])

# Figure 36.31: Entering the Credentials

The Default.aspx page appears (Figure 36.32).

+   9. Click the Log out button to open the Login.aspx again, as shown in Figure 36.32:

![](bbox=[0.23, 0.43, 0.84, 0.74])

# Figure 36.32: Displaying the Default.aspx Page to Authenticated Users

After learning the Forms authentication, let's learn Impersonation in ASP.NET applications.

# Using Impersonation in ASP.NET Applications

Impersonation in ASP.NET is a process in which an ASP.NET application poses as an anonymous or authenticated user to gain access to a resource on the Web server. Impersonation is helpful when the account (NETWORK SERVICE in IIS 7.5 by default) under which the ASP.NET application runs does not have the necessary permissions to access the resource. The application can access the resource by impersonating as a Windows user that has the necessary permissions. In ASP.NET, you can implement impersonation either in the web.config file or through code by using the WindowsIdentity.Impersonate() method. Now, let's demonstrate