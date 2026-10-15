In the preceding line of code, the name of the computer is Server.

# Configuring SqlMembershipProvider

By default, an instance of SqlMembershipProvider, AspNet.SqlMembershipProvider, is defined in the Machine.config file of your ASP.NET application. This instance connects your ASP.NET application to an instance of SQL Server data store running on the local computer. Therefore, if the SQL Server membership data store is installed on a local computer, you do not need to configure SqlMembershipProvider explicitly.

However, if you want to connect your ASP.NET application to an SQL Server data store running on a computer other than the computer on which your ASP.NET application is running, you need to configure SqlMembershipProvider. You can configure SqlMembershipProvider for an ASP.NET application by defining a connection string and an instance of SqlMembershipProvider in the web.config file of the ASP.NET application.

Similar to ActiveDirectoryMembershipProvider, you need to define the <provider> element to create an instance of SqlMembershipProvider. Now, let’s look at some of the common attributes of the <provider> element that you need to set, while defining the <provider> element for SqlMembershipProvider in Table 36.20:

Table 36.20: Attributes of the <provider> Element

| Attribute | Description |
|---|---|
| ApplicationName | Specifies information of the users of a single application. You should qualify the user information with the value of the applicationName, while storing it in the SQL Server data store. This prevents conflicts between similar user names that may arise, while storing information of multiple applications in a single SQL Server data store. The default value of the applicationName attribute is '/'. |
| EnablePasswordReset | Specifies whether or not a user can modify its password. By default, the enablePasswordReset attribute is set to false. You can set this attribute to true only if the requiresQuestionAndAnswer attribute is set to true. |
| PasswordFormat | Specifies the format for storing a password in the SQL Server data store. This attribute can take the following values:
- Clear – Stores the passwords in plain text. It is easy to store and retrieve passwords in this format; however, security of the passwords is compromised.
- Encrypted – Stores the passwords in encrypted form. Decryption needs to be done to retrieve the passwords stored in this format. However, security of the passwords stored in the encrypted format is high.
- Hashed – Hashes the password using a one-way hash algorithm while storing. The security of these passwords is high; however, you cannot retrieve the passwords stored in the hashed format. |
| RequiresQuestionAndAnswer | Specifies whether or not a user needs to provide a password question and answer to modify the password. The default value of this attribute is false. |
| RequiresUniqueEmail | Indicates whether or not e-mail address of the user of an ASP.NET application needs to be unique. The default value of this attribute is false. |

The following code illustrates the configuration of SqlMembershipProvider using the preceding attributes:

```
<configuration>
  <connectionStrings>
    <add name="SqlServices" connectionString="Data Source=localhost;Integrated Security=SSPI;Initial Catalog=aspnetdb;" />
  </connectionStrings>
  <system.web>
    <authentication mode="Forms">
      <forms loginUrl="login.aspx" name=".ASPXFORMSAUTH" />
```