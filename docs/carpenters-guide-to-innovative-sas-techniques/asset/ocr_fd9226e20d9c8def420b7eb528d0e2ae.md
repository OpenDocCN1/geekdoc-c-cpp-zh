# ## 14.2 Using an AUTOEXEC Program

When SAS initializes and starts execution, it automatically looks for and executes (if it exists) a program named AUTOEXEC.SAS. By default the AUTOEXEC.SAS program will only be found if it is in the !SASROOT directory. Through the use of the -AUTOEXEC initialization option (see Section 14.1.1), you can point to any SAS program in any location.

The AUTOEXEC.SAS can be any ordinary SAS program. It is commonly used to set up macro libraries, system options, *librefs*, and *filerefs*. Although the program can be named anything (Fred.jpg), AUTOEXEC.SAS is less obscure.

The AUTOEXEC.SAS shown here could be used to set up the *libref* used to access the data associated with this book. It expects that the automatic macro variable &SYSPARM ❶ was assigned the upper portion of the path structure when SAS was called (see Section 14.1.1 for more

```
```sas
* Autoexec.sas *;
%let path = ❶ &sysparm\InnovativeTechniques;
libname advrpt v9 "&path\Data"; ❷
filename advmac "&path\sasdoc\sasmacros";
options nodate nonumber noncenter; ❸
options sasautos=(advmac, sasautos); ❹
```
```

on the use of the -SYSPARM initialization option). ❷ The *libref* is then established and system options ❸ are declared, including the establishment of the autocall library ❹. This particular AUTOEXEC is short,

but it could just as easily have contained any number of macro calls or even initiated an application.

Typically my Windows desktop contains a different SAS icon for each active client/project. Each has its own unique autoexec program. This ensures that I use the correct data and the correct programs for each project. If you install and use the AUTOEXEC.SAS program that comes with the sample code for this book, the *libref* and autocall macro library used by the sample programs will automatically be available for your use.

# ## 14.3 Using the Configuration File

When SAS initializes, the configuration file is executed *before* the autoexec program. The configuration file is not a SAS program, and if you make changes, the editing must be done carefully. Some companies use the configuration file to provide common setup instructions to all the site's SAS installations and consequently do not allow the modification of this file.

If you do want to customize this file, I would suggest that you do not modify the original version, which can be found in the !SASROOT location. Instead you can copy and then edit the copy. You then point to the modified configuration file using the -CONFIG initialization option (see Section 14.1.1).

The default name for this file is SASV9.CFG. The location will vary according to OS and installation. Under a standard Windows setup, you may find it at one of the following locations:

+   - SAS 9.1   C:\Program Files\SAS\SAS 9.1\nls\en
+   - SAS 9.2   C:\Program Files\SAS\SASFoundation\9.2\nls\en
+   - SAS 9.3   C:\Program Files\SASHome\SASFoundation\9.3