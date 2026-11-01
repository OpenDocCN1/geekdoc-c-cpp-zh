# The Installer Class

The class ProjectInstaller is derived from System.Configuration.Install.Installer. This is the base class for all custom installers. With the Installer class, it is possible to build transaction-based installations. With a transaction-based installation, it is possible to roll back to the previous state if the installation fails, and any changes made by this installation up to that point will be undone. As you can see in Figure 25-9, the Installer class has Install(), Uninstall(), Commit(), and Rollback() methods, and they are called from installation programs.

The attribute {RunInstaller(true)} means that the class ProjectInstaller should be invoked when installing an assembly. Custom action installers, as well as installutil.exe (which is used later in this chapter), check for this attribute.

InitializeComponent() is called inside the constructor of the ProjectInstaller class:

```
using System.ComponentModel;
using System.Configuration.Install;

namespace Wrox.ProCSharp.WinServices
{
    [RunInstaller(true)]
    public partial class ProjectInstaller: Installer
    {
        public ProjectInstaller()
        {
            InitializeComponent();
        }
    }
}
```

code snippet QuoteService\ProjectInstaller.cs

# Process Installer and Service Installer

Within the implementation of InitializeComponent(), instances of the ServiceProcessInstaller class and the ServiceInstaller class are created. Both of these classes derive from the ComponentInstaller class, which itself derives from Installer.

Classes derived from ComponentInstaller can be used with an installation process. Remember that a service process can include more than one service. The ServiceProcessInstaller class is used for the configuration of the process that defines values for all services in this process, and the ServiceInstaller class is for the configuration of the service, so one instance of ServiceInstaller is required for each service. If three services are inside the process, you need to add ServiceInstaller objects — three ServiceInstaller instances are needed in that case:

```
partial class ProjectInstaller
{
    /// <summary>
    /// Required designer variable.
    /// </summary>
    private System.ComponentModel.IContainer components = null;

    /// <summary>
    /// Required method for Designer supportDo not modify
    /// the contents of this method with the code editor.
    /// </summary>
    private void InitializeComponent()
    {
        this.serviceProcessInstaller1 =
            new System.ServiceProcess.ServiceProcessInstaller();
        this.serviceInstaller1 =
```