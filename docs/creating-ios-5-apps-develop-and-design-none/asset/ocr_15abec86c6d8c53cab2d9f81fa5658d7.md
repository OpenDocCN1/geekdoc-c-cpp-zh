The Supporting Files subgroup contains a variety of secondary files. Initially, this group contains the application's Hello World-Info.plist, InfoPlist.strings, main.m, and Prefix.pch files.

The Hello World-Info.plist file contains a number of key-value pairs used to configure our application. The InfoPlist.strings file contains localized versions of the Hello World-Info.plist file's keys. This can be useful when localizing your application, though the file is initially empty. The main.m file contains the main() function, the initial function that is executed when your application launches. The Prefix.pch file is the application's precompiled header.

To help large projects compile faster, Xcode allows us to create a precompiled prefix header file containing a number of #import, #include, and #define directives common across much of our code. For example, in a typical iOS project, most classes need to access the UIKit and Foundation frameworks. By including the #import statements for these frameworks in our prefix header, Xcode knows to preprocess those files and include the results in all of our source files. This prevents the compiler from processing common files multiple times during each build.

This may not make a lot of sense right now, and that's OK. We will not be touching the Prefix.pch file in this project. For more information, check out Apple's documentation: Xcode Build System Guidelines; Reducing Build Times; and Using a Precompiled Prefix Header.

Finally, the Frameworks group contains any iOS frameworks used by this project, while the Products group contains the end results—in this case, our compiled application. Again, we won't be touching any of these in this project.

**NOTE:** Much like Xcode's workspaces, the navigator's groups represent a virtual organization—they exist only within Xcode. These groups do not necessarily have any relationship with how or where the actual resources are stored, or even with what type of files they contain. You are free to place any resource in any group and to add or remove groups or subgroups as needed.

![](bbox=[0.0, 0.7, 0.25, 0.85])