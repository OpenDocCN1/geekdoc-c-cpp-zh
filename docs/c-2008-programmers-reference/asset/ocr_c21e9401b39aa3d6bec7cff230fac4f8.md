In Windows Forms, a feature known as *application settings* allows you to store information persistently in a structured manner without resorting to using a database or forcing you to manually save it to a file. So let's see how application settings can help you in this instance.

Right-click on the *PhotoViewer* project in Solution Explorer and select Properties. In the Properties page, click on the Settings tab and enter the three application settings in the following table (see Figure 16-7).

| Name | Type | Scope | Value |
|---|---|---|---|
| FTP_SERVER | string | User | ftp://127.0.0.1 |
| UserName | string | User | anonymous |
| Password | string | User | password |

![](bbox=[0.25, 0.36, 0.83, 0.78])

**Figure 16-7**

As their names suggest, FTP_Server stores the name or IP address of the FTP server, UserName stores the username used to log in to the FTP server, and Password stores the password used to log in to the FTP server.