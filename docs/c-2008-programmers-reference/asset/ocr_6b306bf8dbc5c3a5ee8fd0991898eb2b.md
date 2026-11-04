# Part II: Application Development Using C#

Add the following files (see Figure 18-40):

+   - SmartDeviceCab1\Release\RSSReader.CAB
+   - RSSReaderInstaller\bin\Release\RSSReaderInstaller.dll
+   - RSSReaderInstaller\setup.ini

![](bbox=[0.38, 0.3, 0.64, 0.55])

These three files will be copied to the user's computer during the installation.

The next step is to configure the MSI installer to perform some custom actions during the installation stage. Right-click the RSSReaderSetup project in Solution Explorer, and select View → Custom Actions (see Figure 18-41).

![](bbox=[0.35, 0.68, 0.68, 0.92])

The Custom Actions tab displays. Right-click on Custom Actions, and select Add Custom Action (see Figure 18-42).