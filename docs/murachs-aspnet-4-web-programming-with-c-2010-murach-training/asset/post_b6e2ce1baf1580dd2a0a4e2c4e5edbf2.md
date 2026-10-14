
## Common certification authorities that issue digital secure certificates

```
www.verisign.com
www.geotrust.com
www.entrust.com
www.thawte.com
```

## SSL strengths

| Strength | Pros and cons |
|---|---|
| 40-bit | Most browsers support it, but it’s relatively easy to break the encryption code. |
| 56-bit | It’s thousands of times stronger than 40-bit strength and most browsers support it, but it’s still possible to break the encryption code. |
| 128-bit | It’s over a trillion times a trillion times stronger than 40-bit strength, which makes it extremely difficult to break the encryption code, but it’s more expensive and not all browsers support it. |
| 256-bit | It’s much stronger than 128-bit encryption, but it’s not supported by all web servers and browsers. |

## Description

- To use SSL in your web applications, you must first purchase a digital secure certificate from a trusted *certification authority*, or *CA*. Once you obtain the certificate, you send it to the people who host your web site so they can install it on the server.
- A certification authority is a company that issues and manages security credentials. To verify information provided by the requestor of the secure certificate, a CA must check with a *registration authority*, or *RA*. Once the registration authority verifies the requestor’s information, the certification authority can issue a digital secure certificate.
- Since SSL is built into all major browsers and web servers, installing a digital secure certificate enables SSL.
- *SSL strength* refers to the length of the generated key that is created during the encryption process. The longer the key, the more difficult it is to break the encryption code.
- The SSL strength that’s used depends on the strength provided by the certificate, the strength supported by the web server, and the strength supported by the browser. If a web server or browser isn’t able to support the strength provided by the certificate, a lesser strength is used.
- Most certificates are issued by trusted certification authorities who own and use their own certificates. These CAs are known to browser vendors, and their certificates have been added to many of the most popular browsers. This type of certificate is called a *single root certificate*.
- A *chained root certificate* is one that inherits the recognition of a trusted certification authority. This type of certificate is more difficult to install and some web servers and web applications can’t use them.

## How to work with certificates using IIS 7

Figure 18-4 shows you how to work with certificates using IIS 7, the version of IIS that comes with Windows 7, Windows Vista, and Windows Server 2008. At the top of this figure, you can see the IIS Management Console with the Server Certificates window displayed. Here, a self-signed certificate named Test certificate has been installed.

A self-signed certificate is simply a certificate that IIS creates for its own use, and you can use it to test security as you develop a web site. Then, if you deploy the web site to a server that doesn’t already have a digital secure certificate installed, you can request a certificate from a certification authority and install it as described in this figure.

To use the HTTPS protocol with IIS 7, a binding must exist for that protocol. A binding defines how a web site can be accessed, and each web site is defined with a binding that uses the HTTP protocol by default. To use SSL with a web site, you must define a binding that uses the HTTPS protocol. When you define that binding, you must also select the certificate you want to use as described in this figure.

## The IIS Management Console with a self-signed certificate installed

![](img/c024ccf88e28c30c07dd410d4342288f_634_0.png)

## How to create and install certificates

- IIS 7 lets you create a *self-signed certificate* that can be used for testing purposes. To do that, display the Server Certificates window. Then, click Create Self-Signed Certificate in the Actions pane and complete the dialog box that’s displayed.
- To create a certificate file that you can use to request a certificate from a certification authority, click Create Certificate Request in the Actions pane and complete the dialog boxes that are displayed.
- To install a certificate from a certification authority, click Complete Certificate Request in the Actions pane and complete the dialog box that’s displayed.

## How to create a binding for the HTTPS protocol

- Before you can use the HTTPS protocol, you must create a *binding* for that protocol. To do that, select the Default Web Site node in the Connections pane, click Bindings in the Actions pane, and click the Add button in the dialog box that’s displayed. Then, select https from the Type drop-down list, select a certificate from the SSL Certificate drop-down list, and click the OK button.

## The IIS Certificate Wizard options if a certificate hasn’t been requested or installed

![](img/c024ccf88e28c30c07dd410d4342288f_636_0.png)

## How to display the IIS Management Console

- Open the Control Panel, double-click on Administrative Tools, and then double-click on Internet Information Services.

## How to determine if a digital secure certificate is installed on your server

- Expand the node for the server and the Web Sites node and then right-click on the Default Web Site node and select Properties to display the Properties dialog box. Click the Directory Security tab. If a digital secure certificate is installed, the View Certificate button will be enabled. Click this button to display the certificate.

## How to get a trial certificate

- To test SSL connections in a local environment, you can request a free trial certificate from an established certification authority. The certificate typically expires in 14 to 30 days.
- The certification authority’s web site will have detailed instructions you can follow to request, download, and install a trial certificate.

## How to use the IIS Certificate Wizard

- The IIS Certificate Wizard manages the process of requesting certificates from certification authorities and installing certificates in IIS.
- To start the IIS Certificate Wizard, display the Directory Security tab of the Properties dialog box for the Default Web Site node as described above, and then click the Server Certificate button.
- The tasks that are available from the wizard depend on whether a certificate is already installed and whether you have requested a certificate but not installed it. To perform any of these tasks, select the appropriate option from the first IIS Certificate Wizard dialog box and then click the Next button and complete the remaining dialog boxes.

## A dialog box that may be displayed for secure connections

![](img/c024ccf88e28c30c07dd410d4342288f_638_0.png)

## A URL that requests a secure connection

```
https://localhost/aspnet_2010/Ch18HalloweenStore/CheckOut1.aspx
```

## A web.config file that defines the AppPath setting

```xml
<?xml version="1.0"?>
<configuration>
    <appSettings>
        <add key="AppPath"
             value="//localhost/aspnet_2010/Ch18HalloweenStore/" />
    </appSettings>
    <system.web>
    .
    .
```

## Code that retrieves the application path from the web.config file

```csharp
string url = "https:"
    + ConfigurationManager.AppSettings["AppPath"]
    + "CheckOut1.aspx";
Response.Redirect(url);
```

## Code that returns to an unsecured connection

```csharp
string url = "http:"
    + ConfigurationManager.AppSettings["AppPath"]
    + "Order.aspx";
Response.Redirect(url);
```

## Description

- To request a secure connection, you must use an absolute URL that specifies HTTPS as the protocol. Once you establish a secure connection, you can use relative URLs to continue using the secure connection.
- To return to an unsecured connection after using a secure connection, you must code an absolute URL that specifies the HTTP protocol.
- Instead of coding the application’s path into each URL, you can store it in the appSettings section of the web.config file. That way, if the path changes, you can change it in just one location.
- You can use the AppSettings property of the ConfigurationManager class within the application to access the elements in the appSettings section of the web.config file.
- Depending on the security settings in your browser, a dialog box may be displayed before a secure connection is established or before a secure connection is closed.

Figure 18-6    How to request a secure connection
