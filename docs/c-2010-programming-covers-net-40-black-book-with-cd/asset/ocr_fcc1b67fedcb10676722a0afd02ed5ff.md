Now, you have learned the implementation of Windows authentication. Let’s learn about the Forms authentication.

# Using Forms Authentication in ASP.NET

Forms authentication has substantial use in the commercial ASP.NET applications and sites, such as those that pertain to online shopping, banking, and e-mailing. In Forms authentication, when a user requests for a protected Web page in the ASP.NET application or site and passes through IIS, the ASP.NET application checks if the user is unauthenticated. In the case of an unauthenticated user, the user is redirected to a login page where the user needs to provide the credentials (user name and password). The credentials provided by the user are then validated against the credentials stored in a given database or the web.config file of the ASP.NET application or site. If the credentials match, then the user gets access to the requested Web page; otherwise, the user is again redirected to the login page.

Let’s create an ASP.NET website and save it as FormsAuth (on the CD-ROM).

The website has two Web pages, Default.aspx and Login.aspx. The Default.aspx page is the protected Web page that requires users to be authenticated before they can access it and Login.aspx is the login page where users provide credentials for authentication. Let’s create the website by performing the following steps:

+   1. Enable the Forms authentication option in IIS for the FormsAuth website.

+   2. Open the web.config file of the FormsAuth website for enabling Forms authentication in the website. Add the following code in the web.config file to enable Forms authentication in the application, and change the <authentication> and <authorization> elements:

```
<authentication mode="Forms">
<forms name="FormsAuthCS" path="/" loginUrl="Login.aspx" protection="All" timeout="30">
<credentials passwordFormat="Clear">
<user name="Harry" password="testHarry" />
<user name="Tom" password="testTom" />
<user name="John" password="testJohn" />
</credentials>
</forms>
</authentication>
<authorization>
<deny users="?"/> <!--denying access to anonymous users-->
</authorization>
```

The mode attribute of the <authentication> element is set to Forms. The <forms> element contains a <credentials> element that contains three <user> elements that specify the valid user names and passwords. In the <authorization> element, the <deny> element is used to deny access to the anonymous users. Therefore, only authenticated users have access to the Default.aspx page.

+   3. Add the code given in Listing 36.16 in the Default.aspx page to design the user interface (UI) of the Default.aspx page:

# Listing 36.16: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Using Forms Authentication</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="label1" runat="server" style="z-index: 100; position: absolute; top: 30px; left: 150px; width: 200px"/>
<br /><br /><br />
```