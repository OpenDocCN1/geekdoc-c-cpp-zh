+   - Under the Device page of the Project Properties dialog, select Pocket PC Device from the Deployment Device combo box.
+   - From the Property window, set the Deployment Device property of the project to Pocket PC Device.

# 28.5.2.4  Requirements for Application Deployment on a Device

+   - Applications built with Visual Studio .NET require that the .NET Compact Framework be resident on the target device. In addition, if the application makes use of SQL Server CE, the SQL Server CE components are required to be installed.
+   - The setup routine takes care of all of these requirements. It may need to include multiple CAB files, one for the application, a second for the .NET Compact Framework and the SQL Server CE CABs.

# 28.5.2.5  Desktop Setup Creation for .NET Compact Framework Application

+   - The installation process becomes slightly more complex if the application setup will be performed from a desktop PC, through a docking cradle to a device. In this situation, there is a need of two setups, one for the desktop PC and one for the device. The device setup is the CAB file. The desktop setup is an executable that performs two functions. First, it copies the CAB files onto the desktop PC. Second, it starts copy Application Manager (CeAppMgr.exe). Application Manager then takes over to copy the CAB file to the device and subsequently launches the installation process.
+   - Application Manager handles adding and removing applications from devices as well as deleting application files from the PC that initiated the installation. The .INI files can be used to provide installation instructions to Application Manager.
+   - Desktop setups can be created for any application that allows to copy CAB files to PC and then the Application Manager can be launched. Two companies, **InstallShield** and **Wise**, provide commercial-grade installation development packages that provide this functionality. **Spb Software House** offers a free setup product called EZSetup. While this application is not as robust as the products from InstallShield and Wise, it functions quite well for most setups.
+   - It should be noted if while writing own desktop setup one has to find where Application Manager is located on the installation PC. The full name and path of Application Manager is stored in the registry value of `HKLM\\Software\\Microsoft\\Windows\\CurrentVersion\\App Paths\\CEAppMgr.exe`.