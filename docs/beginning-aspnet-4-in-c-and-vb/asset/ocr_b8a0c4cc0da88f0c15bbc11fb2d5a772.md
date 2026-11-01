```
new System.ServiceProcess.ServiceInstaller();
// serviceProcessInstaller1
//
// this.serviceProcessInstaller1.Password = null;
// this.serviceProcessInstaller1.Username = null;
//
// serviceInstaller1
// this.serviceInstaller1.ServiceName = "QuoteService";
//
// ProjectInstaller
// this.Installers.AddRange(
// new System.Configuration.Install.Installer[]
// {
// this.serviceProcessInstaller1,
// this.serviceInstaller1;
// }
// )
private System.ServiceProcess.ServiceProcessInstaller serviceProcessInstaller1;
private System.ServiceProcess.ServiceInstaller serviceInstaller1;
```

code snippet QuoteService/ProjectInstaller.Designer.cs

ServiceProcessInstaller installs an executable that implements the class ServiceBase. ServiceProcessInstaller has properties for the complete process. The following table explains the properties shared by all the services inside the process.

| PROPERTY | DESCRIPTION |
|---|---|
| Username, Password | Indicates the user account under which the service runs if the Account property is set to ServiceAccount.User. |
| Account | With this property, you can specify the account type of the service. |
| HelpText | HelpText is a read-only property that returns the help text for setting the username and password. |

The process that is used to run the service can be specified with the Account property of the ServiceProcessInstaller class using the ServiceAccount enumeration. The following table explains the different values of the Account property.

| VALUE | MEANING |
|---|---|
| LocalSystem | Setting this value specifies that the service uses a highly privileged user account on the local system, and acts as the computer on the network. |
| NetworkService | Similarly to LocalSystem, this value specifies that the computer's credentials are passed to remote servers, but unlike LocalSystem, such a service acts as a non-privileged user on the local system. As the name implies, this account should be used only for services that need resources from the network. |
| LocalService | This account type presents anonymous credentials to any remote server and has the same privileges locally as NetworkService. |
| User | Setting the Account property to ServiceAccount.User means that you can define the account that should be used from the service. |