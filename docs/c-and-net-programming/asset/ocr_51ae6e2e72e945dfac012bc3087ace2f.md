# 21.11.2 Global.asax

+   1. **Global.asax** is a file used to declare application-level events and objects. Global.asax is the ASP.NET extension of the ASP Global.asa file. **Code to handle application events** (such as the start and end of an application) reside in Global.asax.
+   2. The Global.asax file must reside in the IIS virtual root. Remember that a virtual root can be thought of as the container of a web application. Events and state specified in the global file are then applied to all resources housed within the web application.
+   3. The Global.asax file is compiled upon the arrival of the first request for any resource in the application.

# 21.11.3 Application Directives

Application directives are placed at the top of the Global.asax file and provide information used to compile the global file. Three application directives are defined, namely Application, Assembly, and Import. Directive has syntax;

```
```
<%@ appDirective appAttribute=Value ...%>
```
```

# 21.11.4 Machine.config File

+   1. The machine.config file is the master configuration file on system with a lot of default settings.
+   2. The settings of Machine.config file are applied to the whole ASP.NET applications on the server.
+   3. Each .NET Framework version has only one machine.config file , at the same time.
+   5. The machine.config file is at the highest level in the configuration hierarchy.
+   6. The machine.config is useful for sharing values between many applications on the server such as SMTP server settings.
+   7. If there are changes in machine.config the application needs to be restarted.
+   8. The machine.config file is automatically installed when Visual Studio.NET is installed and it resides in the c:\windows\microsoft.NET\framework\version\config folder.
+   9. Machine.config is configuration file for all the application in the IIS.

# 21.11.5 web.config File

+   1. Web.config is the file for the local settings to be applied for a website which store configuration data in XML format.
+   2. The settings made in the Web.config file are applied to the particular web application.
+   3. Every web application has its own web.config file.