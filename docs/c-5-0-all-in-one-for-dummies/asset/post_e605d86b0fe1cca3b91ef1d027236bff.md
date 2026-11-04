
more time worrying about crackers. Because you're making a server — usually something you keep private — available to the public, your programs are subject to a whole new set of security rules.

The key to protecting a public server is honesty. You have to be honest with yourself about the weaknesses of the system. Don't think, "Well, a cracker could figure out the password by doing XYZ, but no one would ever do that." Trust me, someone will figure it out.

The two main types of attacks to be concerned about for a Web Forms application are SQL Injection attacks and script exploits.

## SQL Injection attacks

A SQL Injection attack happens when a hacker enters a line of SQL code into an input field used to query a database in a form on a Web page (such as the username and password text boxes in a login form). Malicious SQL code causes the database to act in an unexpected way or to allow the hacker to gain access to, alter, or damage the database.

The best way to understand how a hacker uses a SQL Injection is to see an example. For instance, a web page has code that accepts a Product ID from the user in a text box and returns product details based on the Product ID the user entered. The code on the server might look like this:

```csharp
//Get productId from user
string ProductId = TextBox1.Text;
//Get information from the database
string SelectString = "SELECT * FROM Items WHERE ProductId = '" + ProductId + "' ";
SqlCommand cmd = new SqlCommand(SelectString, conn);
conn.Open();
SqlDataReader myReader = cmd.ExecuteReader();
//Process results
myReader.Close();
conn.Close();
```

Normally, a user enters the appropriate information into the text box. But a cracker attempting a SQL Injection attack would enter the following string into textBox1:

```
*'FOOBAR';--DELETE FROM Items;--'
```

The SQL code that would be run by your code would look like this:

```sql
SELECT * FROM Items WHERE ProductID = 'FOOBAR';DELETE FROM Items;--'
```

The SQL Server executes some code you didn't expect; in this case, the code deleted everything in the Items table.

Book III
Chapter 1
Writing Secure Code

![](img/80ff26f06fc9ab951e1cd4257b867366_439_0.png)

The easiest way to prevent SQL Injection is to never use string concatenation to generate SQL. Use a stored procedure and SQL parameters. You can read more about that in Chapter 2 of this minibook.

## Script exploits

A script exploit is a security flaw that takes advantage of the JavaScript engine in a user’s web browser. Script exploits take advantage of one of the more common features of public Web Forms applications — enabling interaction among users. For instance, a Web Forms application may enable a user to post a comment that other users of the site can view, or it may allow a user to fill out an online profile.

If a malicious user were to put some script code in his profile or comment, that hacker could take over the browser of the next user who comes to the site. Several outcomes are possible, and none of them are good.

For instance, the cookies collection is available to JavaScript when a user comes to your site. A malicious user would put some script code in his profile that could copy the cookie for your site to a remote server. This could give the malicious user access to the current user’s session because the session identifier is stored as a cookie. The malicious user would then be able to spoof the current user’s identity.

Fortunately, ASP.NET prevents users from typing most script code into a form field and posting it to the server. Try it with a basic Web Forms project by following these steps (you see the error shown in Figure 1-3):

- 1. **Create a new Web Forms project.**
- 2. **Add a text box and a button to the default page.**
- 3. **Run the project.**
- 4. **Type `<script>msgbox()</script>` into the text box.**
- 5. **Click the button.**

![](img/80ff26f06fc9ab951e1cd4257b867366_439_1.png)

Additionally, you can use the Server.HtmlEncode method to encode anything that the Web Forms application sends to the screen — this will make script code appear in real text rather than in HTML.

## Best practices for securing Web Forms applications

Aside from making sure that your Web Forms application will prevent SQL Injection attacks and script exploits, you should keep in mind some good practices for securing your web applications.

![](img/80ff26f06fc9ab951e1cd4257b867366_440_0.png)

**Figure 1-3:**
Script exploits are blocked by default.

The following list runs down some of the most important practices for securing your web applications.

- Keep your Internet Information Server (IIS) box up to date.
- Back up everything.
- Avoid using a Querystring variable (the values after the page name in a URL).
- Don’t leave HTML comments in place. Any user can view the HTML code and see your comments by choosing View→Source in a browser.
- Don’t depend on client-side validation for security — it can be faked.
- Use strong passwords.
- Don’t assume what the user sent you came from your form and is safe. It is easy to fake a form post.
- Make sure that error messages don’t give the user any information about your application. E-mail yourself the error messages instead of displaying them to the user.
- Use Secure Sockets Layer.
- Don’t store anything useful in a cookie.
- Close all unused ports on your web server.
- Turn off SMTP on IIS unless you need it.
- Run a virus checker if you allow uploads.
- Don’t run your application as Administrator.

- Use temporary cookies, if possible, by setting the expiration date to a past date. The cookie will stay alive only for the length of the session.
- Put a size limit on file uploads. You can do it in the Web.Config file:

```xml
<configuration>
    <system.web>
        <httpRuntime maxRequestLength="4096" />
    </system.web>
</configuration>
```

- Remember that the ViewState of Web Forms is easily viewable.

## Using System.Security

Although many of the security tools are built into the classes that use them, some classes defy description or classification. For that reason, System.Security is the holding pot for stuff that doesn't fit anywhere else.

The more common namespaces for System.Security are described in Table 1-1. I show how to use the Security.Principal namespace in the earlier section “Authentication using Windows login.”

|  |  |  |
|---|---|---|
| **Table 1-1** | **Common Namespaces in System.Security** |  |
| *Namespace* | *Description* | *Common Classes* |
| Security | Base classes for security | CodeAccessPermission, SecureString |
| AccessControl | Sophisticated control for authorization | AccessRule, AuditRule |
| Authorization | Enumerations that describe the security of an application | CipherAlgorithmType |
| Cryptography | Contains several namespaces that help with encryption | CryptoConfig, DESCryptoServiceProvider |
| Permissions | Controls access to resources | PrincipalPermission, SecurityPermission |
| Policy | Defends repudiation with classes for evidence | Evidence, Site, Url |
| Principal | Defines the object that represents the current user context | WindowsIdentity, WindowsPrincipal |

## Chapter 2: Accessing Data

### In This Chapter

- Understanding the System.Data namespace
- Connecting to a data source
- Exploring the Entity Framework
- Working with data from databases

Not to predispose you to the contents of this chapter, but you’ll probably find that data access is the most important part of your use of the .NET Framework. You’ll likely use the various features of the System.Data namespace more than any other namespace.

Unquestionably, one of the most common uses of Visual Studio is the creation of business applications. Business applications are about data. This is the black and white of development with Visual Studio. While understanding a little of everything is important, complete understanding of the System.Data namespace is essential when you’re building business applications.

Until the .NET Framework became popular in the 2003 timeframe, most business applications built using Microsoft products used FoxPro or Visual Basic. C# has unquestionably replaced those languages as the business programmer’s language of choice over the past several years.

You can look at the data tools in C# in three ways:

- **Database connectivity:** Getting information out of and into a database is a primary part of the System.Data namespace.
- **Holding data in containers within your programs:** The DataSet, DataView, and DataTable containers are useful mechanisms for accomplishing the holding of data. If you’re a Visual Basic 6 or ASP programmer, you may remember Recordsets, which have been replaced by the new constructs. The Language Integrated Query enables you to get the data out of the data containers using Structured Language Queries (SQL) rather than complicated object-oriented language (OOL).
- **Integration with data controls:** The System.Web and System.Windows namespaces function to integrate with the data controls. Data

![](img/80ff26f06fc9ab951e1cd4257b867366_442_0.png)
