Web configuration files are hierarchical; folders inherit authorization rules from their parents and can override them with their own Web.config files. So with traditional ASP.NET WebForms web applications, you would typically implement security by placing pages that can be accessed only by certain users in a separate subfolder and giving it its own Web.config file. For example, you could have created a subfolder called Customers, and placed all custom pages that display customer information in it, along with the following Web.config file, to allow access only for users in the Manager role:

```
```xml
<?xml version="1.0"?>
<configuration>
  <system.web>
    <authorization>
      <allow roles="Manager"/>
      <deny users="*"/>
    </authorization>
  </system.web>
</configuration>
```
```

Because Dynamic Data applications rely on URL routing, there are no physical folders that represent entities—and no Customers folder in the sample application. Therefore, you cannot simply create new configuration files for them. Instead, you can specify authorization rules in the main Web.config of the application, with the help of the <location> element. Here is a configuration file that implements the same authorization rules: Only authenticated users are allowed to access the root of the application, and only users in the Manager role are allowed to access the Customers pages:

```
```xml
<?xml version="1.0"?>
<configuration>
  <system.web>
    <authorization>
      <deny users="?"/>
    </authorization>
  </system.web>
  <location path="Customers">
    <system.web>
      <authorization>
        <allow roles="Manager"/>
        <deny users="*"/>
      </authorization>
    </system.web>
  </location>
</configuration>
```
```

You can further tailor access rights for the Customer entity by creating authorization rules for specific dynamically generated pages. For instance, by adding the following configuration snippet to this Web.config file, you can extend the authorization rules and allow users in the Employee role to access the dynamic Customers/List.aspx page. In other