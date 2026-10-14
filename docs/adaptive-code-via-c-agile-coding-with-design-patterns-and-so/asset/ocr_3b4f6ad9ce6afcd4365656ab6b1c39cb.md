```
<version>1.0.0</version>
<authors>Gary McLean Hall</authors>
<requireLicenseAcceptance>false</requireLicenseAcceptance>
<description>My package description.</description>
<dependencies>
    <dependency id="CorrugatedIron" version="1.0.1" />
</dependencies>
</metadata>
</package>
```

NuGet is such a productivity and organizational bonus that it is painful to return to manually managing third-party dependencies, if a package does not exist for a particular library. In fact, NuGet is not only for third-party dependencies. When a solution becomes large enough it is advisable to split the solution into multiple parts, sliced by layer. The assemblies for each layer can then be packaged by using NuGet and consumed by layers above. This keeps solutions small and easy to work with.

# Chocolatey

The best way to describe Chocolatey is that it is a package management tool, just like NuGet, but its packages are applications and tools, not assemblies. Developers with some Linux knowledge will find that Chocolatey is like apt-get, which is Debian and Ubuntu’s package manager. Again, many of the benefits of package management apply: simplified installation, dependency management, and ease of use.

The following Windows PowerShell script can be used to download and install Chocolatey.

Click here to view code image

```
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

After Chocolatey is installed, you can use the command line to search for and install various applications and tools. The installation procedure will have already updated the command-line path to include the chocolatey.exe application. Much like Git, Chocolatey has subcommands such as list and install, but these also have synonyms that can be used as shortcuts: clist and cinst, respectively. Listing 2-22 shows a sample Chocolatey session that finds the package name for Filezilla, the FTP client, and then installs it.

# LISTING 2-22 First you search the packages for the application that you want, and then you install it.

Click here to view code image

```
C:\dev> clist filezilla
ferventcoder.chocolatey.utilities 1.0.20130622
filezilla 3.7.1
filezilla.commandline 3.7.1
```