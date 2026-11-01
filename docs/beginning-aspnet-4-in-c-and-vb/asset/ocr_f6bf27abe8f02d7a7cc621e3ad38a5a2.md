| PROPERTY | DESCRIPTION |
|---|---|
| IsApplication | Boolean value that, if true, instructs IIS to create the application root for the folder. |
| LogVisits | Boolean value that, if true, logs visits to the web site in a log file. Maps to the Log Visits property of IIS. |
| Property | The named property that can be accessed at installation time. |
| VirtualDirectory | The virtual directory for the application. This is relative to the web server. |

You might notice that most of these properties are properties of IIS and can be set in the IIS Administrator tool. So, the logical assumption is that to set these properties in the installer, the installer will need to run with administrator privileges. The settings made here can compromise security, so the changes should be well documented.

Other than these properties, the process of creating the deployment package is very similar to the previous client example. The main difference between the two projects is the ability to modify IIS from the installation process. As you can see, you have a great deal of control over the IIS environment.

# Client from Web Server

Another installation scenario is either running the install program from a web site or actually running the application from a web site. Both of these are attractive options if you must deploy an application to a large number of users. By deploying from a web site, you eliminate the need for a distribution medium such as CD-ROMs, DVDs, or even floppy disks. By running the application from a web site or even a network share, you eliminate the need to distribute a setup program at all.

Running an installer from a web site is fairly simple. You use the Web Bootstrapper project compile option. You will be asked to provide the URL of the setup folder. This is the folder in which the setup program is going to look for the .msi and other files necessary for the setup to work. After you set this option and compile the deployment package, you can copy it to the web site that you specify in the Setup folder URL property. At this point, when the user navigates to the folder, she will be able to either run the setup or download it and then run it. In both instances, the user must be able to connect to the same site to finish the installation.

# CLICKONCE

ClickOnce is a deployment technology that allows applications to be self-updating. Applications are published to a file share, web site, or media such as a CD. When published, ClickOnce apps can be automatically updated with minimal user input.

ClickOnce also solves the security permission problem. Normally, to install an application the user needs Administrative rights. With ClickOnce, a user can install and run an application with only the absolute minimum permissions required to run the application.

# ClickOnce Operation

ClickOnce applications have two XML-based manifest files associated with them. One is the application manifest, and the other is the deployment manifest. These two files describe everything that is required to deploy an application.