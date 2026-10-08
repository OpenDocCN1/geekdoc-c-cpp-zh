# Building Secure Windows Applications 405

environments, the most privileged users are managers or administrators — yet another set of roles. In most offices, each employee has her own user account, and each user is assigned to the Windows groups that are appropriate for the roles they plays in the company.

Using Windows security works only if the Windows environment is set up correctly. You can't effectively build a secure application in a workspace with a bunch of Windows XP machines where everyone logs on as the administrator, because you can't tell who is in what role.

Building a Windows application to take advantage of Windows security is straightforward. The goal is to check who is logged on (authentication) and then check that user's role (authorization).

The following steps show you how to create an application that protects the menu system for each user by showing and hiding buttons:

+   1. Start a new Windows Forms Application project by choosing File:New Project and giving your project a descriptive name.

This would work for Windows Presentation Foundation (WPF) too, but it's easier to show in Windows Forms. (Book V is all about named my project Windows Security.)

+   2. Add two buttons to your form — one for Sales Menu, one for Accounting Menu, and one for Manager's Menu.

My example is shown in Figure 1-

![](bbox=[0.128, 0.225, 0.843, 0.888])

![](bbox=[0.897, 0.505, 0.973, 0.638])