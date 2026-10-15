![](bbox=[0.15, 0.07, 0.77, 0.36])

# Figure 36.27: Displaying the Web Page

After learning the Anonymous authentication, let’s learn the Windows authentication.

# Using Windows Authentication in ASP.NET

As you know, Windows authentication is an ideal choice for authentication when you want to host an ASP.NET application on the local computer or Intranet. By default, ASP.NET applications are authenticated using the Windows credentials of the currently logged-in user. You can enable any of the following authentication modes in IIS to implement Windows authentication in an ASP.NET application:

+   - Anonymous authentication
+   - Windows authentication (Integrated)
+   - Basic authentication
+   - Digest authentication

In many cases, the default authentication, Anonymous authentication, in IIS is used with Windows authentication in ASP.NET. In such cases, IIS identifies users as anonymous and ASP.NET identifies users as Windows users. You can either disable Anonymous authentication in IIS or use the <authorization> element in the web.config file to deny access to anonymous users.

Now, let’s create an ASP.NET website and save it as WindowsAuth (on the CD-ROM).

In this website, there are two Web pages, Default.aspx and AddEvent.aspx. The Default.aspx page displays the list of events and the AddEvent.aspx page allows you to add a new event. Perform the following steps to create the WindowsAuth website:

+   1. Add two Web pages, Default.aspx and AddEvent.aspx, in the Web application.
+   2. Open the Design view of the Default.aspx file and first add a GridView control in the Default.aspx page. Then, add an SQL Server Database item, named EventsData, in the project and specify a table, named events, in the database. Include five columns, named ID, EventName, Place, Time, and CreatedBy. Now, bind the GridView control to a new data source representing the events table in the EventsData database. In addition, enable paging and sorting by using the GridView Tasks.
+   3. Add the code, given in Listing 36.13, in the Default.aspx page to add the required controls:

# Listing 36.13: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
```