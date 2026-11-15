# ### 1.1.2 Lesser General Public Licence (LGPL)

The LGPL requires that all changes to the libraries must be published openly (the source code must be made available). It is possible, however, to develop a completely new application that uses the libraries without the requirement of releasing the source. The libraries can be linked with proprietary software whereas had they been licensed under the GPL the libraries could only be used with free programs.

# ### 1.1.3 Licensing under EMBASSY

Developers who do not use the GPL or LGPL licence can still contribute. The EMBASSY collection can include packages that use AJAX or NUCLEUS but under their own licensing conditions. They will be bound by the LGPL of the AJAX and NUCLEUS libraries, but not necessarily by the full GPL.

# ## 1.2 Installation of CVS (Developer's) Release

Only very basic information on EMBOSS installation is included here. For complete instructions see the *EMBOSS Administrator's Guide*. The basic installation steps are:

+   1. Download the EMBOSS source code.
+   2. Configure EMBOSS. The stable release contains a ‘configure’ script for this whereas the developer’s (CVS) version contains the files necessary to create this script.
+   3. Compile EMBOSS. This will generate the executable files from the application source code.
+   4. Set a `PATH` to the executables.
+   5. Test the installation.
+   6. Set up your databases.

# ### Caution

To configure and compile EMBOSS the following GNU configuration tools must be installed on your system:

+   - autoconf
+   - automake
+   - libtool

Your OS will often provide these packages; if not then they can be downloaded (from ftp: ftp.gnu.org/gnu/) as source code and installed (in the order shown above and making sure that each newly installed package is being found, in preference to any older version, before installing the next).

You may hit other software dependencies if, for example, you are developing graphics software; see the *EMBOSS Administrator's Guide* for more information.