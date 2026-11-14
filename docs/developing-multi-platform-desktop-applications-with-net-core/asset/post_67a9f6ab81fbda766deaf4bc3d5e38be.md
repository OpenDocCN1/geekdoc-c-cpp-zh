
The Electron.NET.CLI is the command line tool used to build and package the Electron application, it is not used inside the code of the application (it is a tool). Electron.NET.CLI is mandatory for running your .NET Core Electron.NET application.

You can install this tool with the command line described below (this is a toolset package for dotnet CLI). It can be installed as a global tool for dotnet CLI, extending it with the “electronize” command.

```
C:> dotnet tool install ElectronNET.CLI -g
```

After the setup of Electron.NET.CLI in .NET Core, the command “electronize” is available as a global tool for the dotnet CLI. The “electronize” command will be installed only for a specific .NET Core version, the tool itself is installed in the user folder: %UserProfile%/.dotnet/tool/

But before using the Electron.NET wrapper the .NET Core application developer has to install the prerequisites tools: Node.JS and its dependency NPM.

## 8.3.3 Setup of NPM and Node.JS

NPM stands for Node Package Manager, Node.JS is the JavaScript runtime engine from the Chromium project (developed by Google). Electron.NET requires a version >8.6 of Node.JS. We recommend to install the NodeJS from the dedicated web site (see web address in reference) for getting the latest version of the tools and guaranteeing a proper install on each system.

Here are the reference links for the download of the setup file (and for getting the documentation for each OS reviewed here).

https://www.npmjs.com/get-npm
https://nodejs.org/en

We will review in detail how these tools have to be installed on each platform, because this is a core requirement for the usage of the Electron framework and often constitutes an issue in the building process of the project.

### 8.3.3.1 On macOS

For this platform we recommend to install the version from the Node.js web site (this is the latest and you should not have issue with the version number during the building of the Electron.NET application).

Once it is downloaded you have to install the tool by clicking on it (this is a .pkg file). Here is the form you should get after a successful install of the product

![](img/3d310cc066dda6e2dfa67a650614076f_151_0.png)

Once the installation process is finished, we recommend to reboot the computer (for being sure that every environment variable has been updated) before starting to build the Electron.NET application.

### 8.3.3.2 On Ubuntu

On the Linux system you can install Node.JS using the usual package manager “apt” by using the command below, you will have to install NPM as well since it is not in the same package for this environment.

```
$ sudo apt-get update
$ sudo apt-get install nodejs
$ sudo apt-get install npm
```

Here is how a successful install looks.

```
File Edit View Search Terminal Help
johngubuntu:~$
Get:1 http://us.archive.ubuntu.com/ubuntu bionic/main amd64 libhttp-parser2.7.1
amd64 2.7.1-1build1 [39.8 kB]
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 nodejs amd64 8.10.0.dfsg-2ubuntu0.4 [4.790 kB]
Fetched 5,058 kB in 47s (102 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
libhttp-parser2.7.1
Preparing to unpack .../libhttp-parser2.7.1_2.7.1-1build1_amd64.deb ...
Unpacking libhttp-parser2.7.1 (2.7.1-1build1) ...
Setting up libhttp-parser2.7.1 (2.7.1-1build1) ...
Preparing to unpack .../nodejs_8.10.0.dfsg-2ubuntu0.4_amd64.deb ...
Unpacking nodejs (8.10.0.dfsg-2ubuntu0.4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Setting up nodejs (8.10.0.dfsg-2ubuntu0.4) ...
update-alternatives: using /usr/bin/nodejs to provide /usr/bin/js (js) in auto mode
Processing triggers for libc-bin (2.27-3ubuntu1) ...
root@ubuntu:~#
```

Once both packages have been correctly (without errors) installed
you can control the version installed with the command below.

```
$ nodejs -v
```

The use of this command will also help you to validate if everything
is in working order (verify if the install has been performed
correctly). The version number displayed has to be >8.6.

### 8.3.3.3 On Windows

On Windows, you have to install NPM and Node.js.
The setup of the Node.JS version from the Visual Studio Installer
program is not adapted for the building of an Electron.NET
application (as you also need NPM to be installed). We recommend
to not use this version for this specific task.

The much simpler solution consists in the setup of the
Node.JS/NPM from the dedicated web site, it will ensure you install
the latest version available (the link is provided in reference
previously).

Here is a view of the install program.

![](img/3d310cc066dda6e2dfa67a650614076f_153_0.png)

Windows requires that you reboot the system for updating the system with the new environment variables before starting to use it.

## 8.3.4 Electron.NET QuickStart

The use of Electron.NET implies to follow a procedure in order to integrate it inside an ASP.NET Core application and transform it to a desktop application.

Here is the short procedure for “electronize” your ASP.NET Core 3 application. We will review later in much more detail the application code itself (within the example section).

- A) Create an ASP.NET Core MVC application

That can be done by using the dotnet CLI or Visual Studio.

- B) Install the Electron.NET command line global (since version 0.9) tool

Before starting the development of your application, you have to install the Electron.NET.CLI global tool for the dotnet CLI with the command line described below.

```
$ dotnet tool install --global Electron.NET
```

- C) Add the Electron.NET package:

Besides adding it from Visual Studio NuGet package manager, you can add the dependency by typing the following line in the package manager command line.

```
PM> Install-Package Electron.NET.API
```

### D) Setup packaging (For ubuntu and macOS only)

This step is only for the ubuntu and macOS platform, on these OS you have to install “electron-builder” with the command line instruction as below.

```
$ sudo npm install electron-builder --global
```

### E) Start to use Electron.NET:

You can achieve that by using the following code inside the WebHostBuilder.

```
public static IWebHost BuildWebHost(string[] args)
{
    return WebHost.CreateDefaultBuilder(args)
        .UseElectron(args)
        .UseStartup<Startup>()
        .Build();
}
```

You can notice we have just added the “UseElectron(args)” line to the WebHost for enabling the use of Electron inside the MVC ASP.NET Core application.

### F) Create the Electron window in the Startup.cs file:

This can be done by the following instruction in the “Configure” method:

```
Task.Run(async () => await Electron.WindowManager.CreateWindowAsync());
```

With this line of code, the web application is executed inside an Electron window.

### G) Initialization of the application:

The first time you start the Electron application you have to “initialize” it with the command described below (you have to be in the application folder).

```
::\appPath>dotnet electronize init
```

This command will create the “electron.manifest.json” file that is used by the “electronize” command for the execution of the program (this file describes the Electron context).

### H) Execute the application:

After that, you can execute the Electron.NET ASP.NET Core application with the command “start” as described below (in the application folder for Windows and in the solution folder for ubuntu and macOS).

```
::\appPath>dotnet electronize start
```

On ubuntu and macOS you have to use the “electronize” command without the “dotnet” part as described below.

```
> electronize start
```

With this command the application is executed in a classical desktop application window (not in the browser, but this is still a web application).

## 8.3.5 Electron.NET application example

As Electron.NET is a popular wrapper around Electron, you will find plenty of code examples (check GitHub) for helping and guiding you for the development of your Electron.NET application (see reference links).

These examples make often an intensive use of the SPA (Single Page Application) techniques and use specialized JavaScript frameworks like Vue.JS or React... The reason is that the desktop application experience requires a minimum of blinking screen being liked by the user and looked as a tangible desktop application.

So, the development of an application with Electron.NET implies an intensive use of JavaScript for making the buffer between the web development back-end and the desktop Front-End (which has a natural tendency to blink as a common web application).

The Electron.NET, ASP.NET Core example application we will review is the “ElectronNET-API-Demos” application from the Electron.NET repository.

This is the application of reference for this type of application. It illustrates the use of many Electron.NET features. Most of the source code is exposed in the application itself for teaching purpose.

In this sample, you will find a couple of useful techniques specific to the Electron.NET application type, these techniques can be reused in
