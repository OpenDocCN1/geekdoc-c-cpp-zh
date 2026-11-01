You're likely to use the first scenario when dealing with an external hosting company that hosts your site. When web hosts offer SQL Server, they often use SQL Server Authentication and, as such, require you to pass a username and password to the database server.

The second scenario is useful if you host the site yourself and have both SQL Server 2012 and IIS on the same machine.

More advanced scenarios, such as using Windows Authentication with IIS and SQL Server on two different machines, are beyond the scope of this appendix. For more information about configuring and securing SQL Server, get yourself a copy of Professional Microsoft SQL Server 2012 Administration by Adam Jorgensen, Steven Wort, Ross LoForte, Brian Knight, 2012, (Wrox, ISBN: 978-1-1181-0688-4).

# Scenario 1 — Using SQL Server Authentication

From a configuration point of view, this is probably the easiest scenario to configure: all you need to do is make sure that your SQL Server installation supports SQL Server Authentication, create a user in SQL Server, and then use that account in the connection string of the Planet Wrox website. To do this, follow these steps:

+   1. In SQL Server Management Studio, right-click the server name in the Object Explorer shown in Figure B-3, choose Properties, and switch to the Security category. The dialog box shown in Figure B-4 appears.

![](bbox=[0.18, 0.7, 0.82, 0.92])

FIGURE B-4