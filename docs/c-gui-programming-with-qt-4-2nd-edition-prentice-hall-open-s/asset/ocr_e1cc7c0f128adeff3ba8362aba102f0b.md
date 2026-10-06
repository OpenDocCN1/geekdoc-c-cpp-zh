# Installing Qt/Mac

Before Qt can be installed on Mac OS X, Apple's Xcode Tools must already be installed. The CD (or DVD) containing these tools is usually supplied with Mac OS X; they can also be downloaded from the Apple Developer Connection, http://developer.apple.com/.

If you have Mac OS 10.4 and Xcode Tools 2.x (with GCC 4.0.x) or later, you can use the installer described shortly. If you have an earlier version of Mac OS X, or an older version of GCC, you will need to install the source package manually. This package is called qt-mac-opensource-4.3.2.tar.gz and is available from Trolltech's web site. If you install this package, follow the instructions in the next section for installing Qt on X11.

To use the installer, download qt-mac-opensource-4.3.2.dmg. (This version was correct at the time of this writing, but it will probably be different by the time you read this.) Double-click the .dmg file, and then double-click the package called Qt.mpkg. This will launch the installer, which will install Qt in /Developer, along with its documentation and the standard examples.

To run commands such as qmake and make, you will need to use a terminal window, for example, Terminal.app in /Applications/Utilities. It is also possible to generate Xcode projects using qmake. For example, to generate an Xcode project for the hello example, start a console such as Terminal.app, change to your examples/ chap01/hello directory, and enter the following command:

```
qmake -spec macx-xcode hello.pro
```