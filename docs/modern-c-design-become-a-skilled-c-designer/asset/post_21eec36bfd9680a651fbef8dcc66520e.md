
be practical to implement a graphing calculator for a computer when sophisticated standalone graphing programs exist, the exercise might prove to be a lot of fun. Starting with version 5.7, Qt now includes a graphing module to make this task significantly easier than it would have been previously. Given this graphing widget set, the biggest challenge might simply be devising a method for graphical input. If you’re in the mood for a silly throwback to the 1970s, consider implementing an ASCII graphing calculator for the CLI!

## A Plugin Management System

Currently, plugins are loaded during pdCalc’s startup, and which plugins to load are determined by reading shared library names from a text file. Plugins, once loaded, cannot be unloaded. Consider implementing a dynamic plugin management system so that plugins can be selected, loaded, and unloaded at runtime. You could even extend the plugin interface to enable dynamic querying of plugin descriptions. I think the real gotcha here will be in figuring out how to handle the unloading of a plugin that has one of its commands currently on the undo/redo stack.

## A Mobile Device Interface

In my original machinations for creating this book, I envisioned a chapter describing how to extend pdCalc to an iOS or Android tablet. The Qt library can once again help you with this task. The reason I did not include such a chapter in this book is that I do not have any practical experience with tablet programming. I felt it would be disingenuous to try to teach others how to design a tablet interface from my first-ever foray into that design space. Well, it might have been an excellent example of a bad design! Nonetheless, extending pdCalc to a tablet or smartphone interface is a worthy challenge, and the last one I leave you with.

## APPENDIX A

### Acquiring, Building, and Executing pdCalc

This appendix explains how to acquire and build pdCalc, the program described in this book.

#### Getting the Source Code

The source code for pdCalc is hosted on Apress’s GitHub repository. The easiest way to find the correct repository is through this book’s Apress website:

[http://www.apress.com/us/book/97814842305](http://www.apress.com/us/book/97814842305)

Clicking the Download source code button will take you directly to the GitHub hosted site. Once there, you have two options for downloading the source code. The first option is to use a git client ([https://git-scm.com/](https://git-scm.com/)) and clone the repository to your local computer.

For those familiar with managing source code with git, this is the preferred source code acquisition method. Using git to clone the repository will enable you to pull periodic bug updates from the online repository. Maybe you’ll even decide to contribute a bug fix to pdCalc yourself! The second option for acquiring the source code is to download a single zip file of pdCalc from GitHub. Obviously, downloading a single zip file makes updating the source code significantly more challenging than using git if you have made any local changes.

#### Dependencies

Now that you have the source code, you’ll probably want to build and execute pdCalc and its unit test suite. Before that can be accomplished, however, you’ll need to ensure that you have an appropriate tool chain. Intentionally, pdCalc requires very few external dependencies, in fact, only two, both of which can be obtained for Linux, Windows, or Mac OS X at no cost. In order to build pdCalc, you will need a modern C++ compiler (C++14 compliant) and Qt (version 4 or 5).

As someone willing to have read this book, you probably already have or know how to get a C++ compiler. That said, for simplicity, the build system I provided for pdCalc assumes use of the gcc compiler (mingw in Windows). If you do not have gcc on your Linux system, it should be available through your system’s package manager. If that fails, it can be downloaded from the Free Software Foundation’s website (https://gcc.gnu.org/). On Windows, mingw is bundled with Qt as an optional component. I highly recommend obtaining it through Qt’s installer.

On Linux, Qt, including its native integrated development environment (IDE) named Qt Creator, can usually be obtained through the system’s package manager. If you go this route, ensure that you install the development packages for Qt and not just the runtime libraries. For both Linux and Windows, Qt can also be downloaded from http://www.qt.io/download/. Once you are on the website, select the Desktop and Mobile edition, and then choose the version that is licensed appropriately for your use. pdCalc is distributed under the GPL version 3, so the open source edition of Qt is compatible. From Qt’s download page, you can select a fully downloadable binary installer, a network-based binary installer, or the complete source code. Unless you are experienced in building complex libraries from source, I recommend one of the binary installers. On Windows, be sure to install the mingw compiled version of Qt as well as the mingw tool chain. On all operating systems, while not strictly necessary, I highly recommend also installing Qt Creator. Please be patient with the download. Qt, with its many modules, is a powerful, but very sizable package.

#### Building pdCalc

To avoid additional dependencies, pdCalc object code is built using your tool chain’s native make tool, which, in turn, calls the compiler and linker. For pdCalc, on a Linux system, you’ll use make, which will, in turn, use gcc for compiling and linking. On a Windows system, you’ll use mingw32-make, which will, in turn, use the mingw compiler and linker.

Now that you understand how qmake works, let’s examine how to build pdCalc using either Qt Creator or the command line.

##### Using Qt Creator

If your preference is to use Qt Creator, most of the complexity of using qmake will be hidden from you. To begin, simply launch the IDE, and open the pdCalc.pro project. This file is located at the top level of the source tree.

The first time you open a qmake project file with Qt Creator, you will be presented with a configuration list asking you which version of Qt to target. If you only have one version of Qt on your computer, you may only have one option. If you expand the Details button for your selected Qt version, you will be given the option to configure pdCalc for debug, release, and profile and the option to select a folder as your out-of-source build directory. Once you have selected your configuration options, click the Configure Project button. If you need to change your configuration options later, Qt Creator has a tool for that.

After Qt Creator configures your project, you will be presented with the edit mode for the project. The edit mode of Qt Creator is a good tool for exploring the source code. The complete source tree will appear in an expandable tree control on the left side of the display, and individual files can be opened by clicking them. The source tree for pdCalc is described in Appendix B.

Qt Creator works similarly to any other fully featured IDE you have probably used, and a complete description of its usage is beyond the scope of this Appendix (see http://doc.qt.io/qtcreator/ for the full manual). However, I will highlight a few quick features to help get you started.

The first shortcut to learn is choosing which configuration of your project you want to build and run. These options are selected by the monitor icon in the lower left corner of the display. It will currently be labeled with the active project (pdCalc if it’s the only project loaded) and the current configuration (e.g., Debug or Release). If you click this monitor icon, a pane will open allowing you to select which configuration you wish to build and which executable you wish to run. For pdCalc, you’ll have four executable options: pdCalc, pdCalc-simple-cli, pdCalc-simple-gui, and testDriver. pdCalc runs the full version of pdCalc (the GUI by default), pdCalc-simple-cli runs the simple CLI constructed at the end of Chapter 5, pdCalc-simple-gui runs the simple GUI constructed at the end of Chapter 6, and testDriver runs the unit test suite. If you want to change the build or run configuration options, you can click the Projects button (folder icon) on the
