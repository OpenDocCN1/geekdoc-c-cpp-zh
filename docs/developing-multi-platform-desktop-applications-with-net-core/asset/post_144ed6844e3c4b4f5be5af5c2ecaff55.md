
## 8.5.2 GTK Install

As you understood GTK is a Linux native tool but need to be install on the others system (Windows and macOS). Since the third version the setup of GTK is not a simple binary to launch. The process for the install on Windows and macOS consists in the setup of a Linux emulated environment (the size on use disk for this environment could be as huge as an original ubuntu distribution).

GTK need to be installed on the machine you plan to deploy or test your GTK application too (at least the runtime). We will review in details how you can do this setup on each system.

### 8.5.2.1 On Windows (for the development station)

This description for the setup of GTK come from the gtk.org (see the references web sites) web site. This is the recommended procedure for performing the install of GTK on your Windows platform. Another solution is to build the GTK toolkit from the source code but it will require a prior installation of a C building environment (that's not our purpose here).

### A) Install MSYS2

For the setup of GTK you will need to setup an environment for this type of application: mingw. MinGW is the contraction of “Minimalist GNU for Windows”, it provides the Opensource environment for the development of application for Microsoft Windows.

MSYS2 is a project who provide a Unix like environment on a Windows station (MinGW). This project furnishes the foundation for the development of a GTK application on Windows, it will allow the setup of the GTK runtime and the tools (like Glade) you will need for developing your .NET Core 3 GTK application.

MSYS2 furnish a Unix like package manager, “pacman” and many other useful tools from the Linux environment.

```
https://www.msys2.org/
https://msys2.github.io/
https://www.gtk.org/download/windows.php
https://mingw.org/
```

You can install MSYS2 as a standard windows application as you can see (figure 1, 2, 3). The installation program should not return any error during the setup process if this is the case, uninstall the faulty version, fix the problem and reinstall from the beginning until you reach a clean MSYS2 install.

![](img/3d310cc066dda6e2dfa67a650614076f_186_0.png)

(figure 1)

### Installing MSYS2 64bit

Installing component MSYS2 64bit base...

Show Details

The final screen (figure 3) shows the Mingw command prompt, this screen indicates that the installation is completed and successful.

When the install process is finished, reboot Windows.

### B) Install GTK

Once you have achieved a proper MSYS2 install and rebooted, you should now install GTK runtime and development libraries. This install can be done through the use of the appropriate “pacman” (Package Manager) command in the mingw environment.

```
~ pacman -S mingw-w64-x86_64-gtk3
```

The result expected should look as (figure 4)

![](img/3d310cc066dda6e2dfa67a650614076f_188_0.png)

(figure 4)

### C) Install Glade

Glade is the new GTK interface designer, it will allow you to make the design of your application through a visual tool and save it to a XML standard format file who can be loaded by GTK using the GTKBuilder. In its third version this is a professional class tool who will allow the design of your GTK application GUI as you design a standard C# Winforms application.

Even if Glade has its own logic for the design it allows the developer to achieve a sharp modeling of the GUI.

The setup of Glade is also performed with the “pacman” program by using the following command:

```
~ pacman -S mingw-w64-x86_64-glade
```

The successful installation of Glade screen should look like (figure 5).

![](img/3d310cc066dda6e2dfa67a650614076f_189_0.png)

(figure 5)

Once installed, you can manually launch the Glade program by clicking on the “glade.exe” file in the mingw folder, or running the command line “glade.exe”.

We will review later how to integrate Glade within Visual Studio 2019 for the edition of the interface (XML file) without leaving the IDE.

Of course, if you do not plan to use the GUI visual designer and define the GUI with C# inline code and XML you will not need to install Glade, it is not a mandatory install if you write your GUI by hand.

### D) Configure environment variable

For having a system wide access to the GTK libraries and dependencies you should modify the windows global path. For doing so you have to edit the global path environment variable:

Control Panel > System and Security > System > Advanced system settings > Environment variables >

Modify the “Path” variable by adding “C:\msys64\mingw64\bin” (or the path to the mingw tool you have setup) to it as described on the picture below (figure 6).

![](img/3d310cc066dda6e2dfa67a650614076f_191_0.png)

(figure 6)

This modification will be effective after the next reboot of the Windows system.

You have also the possibility to add the environment variable path only for your GTK application inside Visual Studio project properties but we will review this solution later in the example section.

### TIPS: Alternative method for Gtk installation on Windows

The previous method for the installation has the drawback of being a bit heavy, you have to install the full mingw building environment for achieving it, it can seem a little oversized according to the aim of the install (install of the GTK Runtime). This is because no one (the GTK community is not as active as before) have done the release of a binary install package for the GTK Toolkit since the second version (several years).

Nevertheless, independent programmers provide this kind of setup by using a well factored NullSoft install program. The current install version binary is available on their GitHub.

https://github.com/tschoom/GTK-for-Windows-Runtime-Environment-Installer

This distribution (done by Tom Shoonjans and Alexander Shaduri) integrates the latest available Gtk Toolkit, the version 3.24 and all the dependencies required for make it work properly. This latest version has been released on the 2 July 2019 and seems to be a reliable source for the GTK toolkit installation. You will find also NullSoft scripts for generating your own installer for the GTK runtime on Windows.

## 8.5.2.2 On macOS

As we have previously mentioned, the installation of GTK on macOS can be done through the use of “HomeBrew” (see the reference web links) and by following the process described below.

http://brew.sh/

If you have not installed Brew before, here is how install it and then after how to install GTK with it.

### A) Install Brew

You can install brew by executing the command line in the macOS terminal prompt:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

The result should look like described (figure 7).

![](img/3d310cc066dda6e2dfa67a650614076f_193_0.png)

(Figure 7)

### B) Install GTK

Once Brew is installed you can easily install the GTK runtimes and dependencies with the following command line (formula). This will install the GTK version 3 and all its dependencies.

```
$ brew install gtk+3
```

This command should produce the following output in case of a correct setup of the package.

![](img/3d310cc066dda6e2dfa67a650614076f_194_0.png)

(figure 8)

If you do not obtain a correct installation, as usual, you should fix the eventual issue and reinstall the package from the start.

## 8.5.2.3 On ubuntu

GTK is natively installed on the ubuntu desktop version (it is the tool used for the development of Gnome) thus you will not have to install any additional module for executing the GTK GUI application type. As native component from ubuntu the performances of the GUI will also be better than any other systems.

## 8.5.3 Presentation of GTK#

Now that the GTK runtime is available on each platform, we can start to explain how we will use it from our .NET Core 3 application. The GTK runtime have a .NET wrapper already developed and validated: GTK#.

This toolkit became multiplatform in its latest release (with the adoption of the .NET Standard 2.0 of GTK#) and thus can be used for multiplatform GUI application development with .NET Core 3.

GTK# is a Graphical User Interface toolkit for .NET, this tool allows to .NET developers the use of the GTK+ in .NET.

GtkSharp (that's the pronunciation) is a C# wrapper around GTK and its components, this is a fork of the previous gtk-sharp library who was targeting mono (and Gtk 2.xx).

The latest version of GTK# target the GTK version 3.22 and is available in the .NET Standard format. The source code is under Opensource license and available at the following links on GitHub.

![](img/3d310cc066dda6e2dfa67a650614076f_195_0.png)

The GTK# library is also available through the NuGet package distribution system. Added to the base wrapper GTK#, a dedicated package provides new project template and project items for the development of a GTK# applications with the dotnet CLI tool (works with .NET Core 3).

![](img/3d310cc066dda6e2dfa67a650614076f_195_1.png)
