```
new System.Configuration.Install.Installer[]
    {this.serviceProcessInstaller1,
        this.serviceInstaller1});
}

private System.ServiceProcess.ServiceProcessInstaller
    serviceProcessInstaller1;
private System.ServiceProcess.ServiceInstaller
serviceInstaller1;
}
```

The class ServiceProcessInstaller installs an executable that contains a class that derives from the base class ServiceBase. ServiceProcessInstaller has properties for the complete service process. The following table describes the properties shared by all the services inside the process.

| Property | Description |
|---|---|
| Username, Password | Indicates the user account under which the service runs if the Account property is set to ServiceAccount.User. |
| Account | With this property, you can specify the account type of the service. |
| HelpText | A read-only property that returns the help text for setting the username and password. |

The process that is used to run the service can be specified with the Account property of the ServiceProcessInstaller class using the ServiceAccount enumeration. The following table describes the different values of the Account property.

| Value | Description |
|---|---|
| LocalSystem | Setting this value specifies that the service uses a highly privileged user account on the local system, and acts as the computer on the network. |
| NetworkService | Similarly to LocalSystem, this value specifies that the computer’s credentials are passed to remote servers; but unlike LocalSystem, such a service acts as a nonprivileged user on the local system. As the name implies, this account should be used only for services that need resources from the network. |
| LocalService | This account type presents anonymous credentials to any remote server and has the same privileges locally as NetworkService. |
| User | Setting the Account property to ServiceAccount.User means that you can define the account that should be used from the service. |

ServiceInstaller is the class needed for every service; it has the following properties for each service inside a process: StartType, DisplayName, ServiceName, and ServicesDependentOn, as described in