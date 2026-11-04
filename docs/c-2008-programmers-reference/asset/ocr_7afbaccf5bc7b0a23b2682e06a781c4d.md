The content of the user.config file looks like this:

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <userSettings>
    <PhotoViewer.Properties.Settings>
      <setting name="FTP_SERVER" serializeAs="String">
        <value>ftp://127.0.0.1/</value>
      </setting>
      <setting name="UserName" serializeAs="String">
        <value>anonymous1</value>
      </setting>
      <setting name="Password" serializeAs="String">
        <value></value>
      </setting>
    </PhotoViewer.Properties.Settings>
  </userSettings>
</configuration>
```
```

Each user (of your computer) will maintain his own copy of the user.config file.

# Coding the Application

Now to code the application. Switching to the code-behind of Form1, import the following namespaces:

```
```csharp
using System.Net;
using System.IO;
```
```

Define the WebRequestMethod enumeration:

```
```csharp
namespace PhotoViewer
{
    enum WebRequestMethod
    {
        MakeDirectory,
        DownloadFile,
        ListDirectoryDetails,
        RemoveDirectory,
        DeleteFile
    }
}
```
```

Declare the following constants and member variables:

```
```csharp
public partial class Form1 : Form
{
    //---constants for the icon images---
    const int ico_OPEN = 0;
    const int ico_CLOSE = 1;
    const int ico_PHOTO = 2;
}
```
```

In Form1, select the three TextBox controls (you can Ctrl+click each of them) that ask for the FTP server name, user name, and password (see Figure 16-9). In the Properties window, double-click the Leave property to generate an event handler stub for the Leave event.