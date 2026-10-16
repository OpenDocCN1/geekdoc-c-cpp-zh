
## Turning source code into compiled code and compiled code into an executable

After you have created your source code, you need to have the computer turn your source code into the instructions that it can execute. This part of the process is called compiling the source code.

Compiling the source code actually involves several steps.

The first step is called preprocessing. You can think of the preprocessing step as the computer preparing your code to be compiled. During this step, the compiler removes any code that will not result in executable code such as comments and so on. It also expands parts of the code and rearranges certain directives so that the second step of the compilation process can be more efficient. The end result of the first step of compilation is an intermediate state of the source code. You typically will not see or deal with this intermediate form of the code though there are compiler switches that will cause the compilation to stop at this stage if you wanted to look at the output for whatever reason. Some developers who utilize advanced techniques will sometimes use these compiler switches so that they can look at the intermediate file and see exactly what the compiler is doing. You will probably never have to do that in your normal application development.

After preprocessing, the second step is where the compiler actually turns your source code into what’s called an object file. Object files have an extension of .o. Compiling source code can be a relatively lengthy process, involving many different modules and many different source code files. As a result, if you can avoid rebuilding a particular module in the case where it and none of its dependencies have changed, then this can be a big win in terms of reducing compilation time. Because of this, the object files are typically stored on disk in your build directory. In the case where a source code file did not change since the last time the compiler was run, this enables the compiler to simply skip recompiling that source code and instead reuse the object file that was left from the last run of the compiler. Typically, you will have no need to look at these files in day-to-day use. They are there for the compiler’s use only.

The final step of compilation involves a process called linking. Linking means taking the object files produced in the last step and connecting them together to form an executable. In addition to the objects themselves, libraries and frameworks are also linked into the executable as well. The end result of the linking process is your actual application executable. In the case of a command line application, this will be a single binary file which you can run from the command line. In the case of a desktop application, this will usually be what’s called an application bundle that actually is a directory on disk containing an executable and all the resources such as graphics, sounds, and so on that are necessary for running the application. You learn more about application bundles in the next section.

In Xcode, compiling your app is as simple as hitting the Build and Run button. If you do this with your example project, it’ll launch the application in the console and display its output. While doing so, Xcode switches to debug mode and allows you to debug the application as well. Debugging is an advanced IDE topic; see the Xcode documentation for information on how to use it for debugging.

The end result of the compilation process is your executable. If at any point the compiler detects an error in your source code, then it will halt the processing of the file in question and display the error to you so that you can correct it. Sadly, the compiler is pretty picky. Computers are not nearly as good as we are at inferring meaning from words. As a result, the compiler, rather than guessing at what you meant to type, simply gives up and displays the error to you. These errors can be as simple as a missing semicolon, a missing space, incorrect capitalization, or any number of tiny things. Be prepared — by embarking on a career as a programmer, you will be dealing with errors like this hundreds if not thousands of times a day. Even the best programmers rarely write code that compiles perfectly the first time.

## Exploring application bundles

In the previous section, I mentioned the term application bundle — what may be a completely new term to you even if you are an experienced programmer. You may be wondering what that is. An application bundle is really more related to being an operating system construct than it is to an Objective-C construct. The Objective-C language itself does not require or produce application bundles. That said, however, application bundles are an important and integral concept to programming on almost all the platforms on which Objective-C can be used, and, as a result, they are important concepts for you as an Objective-C programmer to understand.

An application bundle is simply a directory on a disk containing a grouping of files. In Mac OS X, application bundles are used for applications to group together all the files necessary for an application to run. This includes items such as executables, graphics, sound files, and user interface resources. Additionally, when building graphical applications for Mac OS X, the user interface definitions are typically done in an application called Interface Builder. This application also produces bundles called NIB files. NIB files usually have an extension of .nib and are stored inside the application bundle.

### NOTE

NIB stands for NeXTstep Interface Builder and is a holdover from the NeXT days. Recently, the format was changed from binary to XML, and the file extension was changed from .nib to .xib. During compilation, XIB files are still compiled to NIB files, so when you look in an application bundle, you’ll see .nib and not .xib.

Listing 1.3 shows a typical application bundle directory structure. In this case, it’s a partial listing of the Xcode application bundle.

### Contents of an Application Bundle

```
Xcode.app
`-- Contents
|--- CodeResources -> _CodeSignature/CodeResources
|--- Info.plist
|--- Library
|   `-- QuickLook
|       `-- SourceCode.qlgenerator
|           `-- Contents
|           |--- CodeResources -> _CodeSignature/CodeResources
|           |--- Info.plist
|           |--- MacOS
|           |   `-- SourceCode
|           |--- _CodeSignature
|           |   `-- CodeResources
|           `-- version.plist
|   `-- Spotlight
|       |--- SourceCode.mdimporter
|       |   `-- Contents
|       |   |--- CodeResources -> _CodeSignature/CodeResources
|       |   |--- Info.plist
|       |   |--- MacOS
|       |   |   `-- SourceCode
|       |   |--- _CodeSignature
|       |   |   `-- CodeResources
|       |   `-- version.plist
|       `-- uuid.mdimporter
|           `-- Contents
|           |--- CodeResources -> _CodeSignature/CodeResources
|           |--- Info.plist
|           |--- MacOS
|           |   `-- uuid
|           |--- Resources
|           |   |--- English.lproj
|           |   |   |--- InfoPlist.strings
|           |   |   `-- schema.strings
|           |   |--- Japanese.lproj
|           |   |   |--- InfoPlist.strings
|           |   |   `-- schema.strings
|           |   `-- schema.xml
|           |--- _CodeSignature
|           |   `-- CodeResources
|           `-- version.plist
|--- MacOS
|   `-- Xcode
|--- PkgInfo
|--- PlugIns
```

Listing 1.3 (continued)

```
|   |-- BuildSettingsPanes.xcplugin
|   |   `-- Contents
|   |       |-- CodeResources -> _CodeSignature/CodeResources
|   |       |-- Info.plist
|   |       |-- MacOS
|   |       |   `-- BuildSettingsPanes
|   |       |-- Resources
|   |           |-- Built-in Build Settings Panes.pbsettingspanespec
|   |
|   |-- Resources
|   |   |-- AskUserForNewFileDialog
|   |   |-- CreateDiskImage.workflow
|   |   |   `-- Contents
|   |   |       `-- document.wflow
|   |   |-- DevCDVersion.plist
|   |   |-- Document-Cert.icons
|   |-- _CodeSignature
|   |   `-- CodeResources
|   `-- version.plist
```

Note that the directory Contents/MacOS contains the Xcode executable. This executable is the same as one that you would produce if you were making a command line application. The difference here is that it is packaged inside of an application bundle and contains code to load the resources from that bundle. Some other interesting directories inside this application include the PlugIns directory, which has bundles inside of it as well. The Spotlight directory also contains bundles in the form of the SourceCode.mdimporter and uuid.mdimporter directories. The Foundation framework, which we will visit in Part II of this book, includes methods that enable you to read application bundles, and it allows access to these sorts of embedded bundles.

The important thing for you to know at this time is that when you create a graphical application for Mac OS X, iPhone, or iPad, Xcode creates an application bundle for your application. In the future, if you have the need to include compartmentalized groupings of resources within your application, you may want to create an application bundle yourself. Xcode also gives you the ability to do exactly that. For now, however, you don't need to worry about that.

## Working with build settings

There are two locations in Xcode where build settings for your projects are configured. The first and primary location is the project information window, which you access by choosing Project ▷ Edit Project Settings. In this section, I cover these windows in detail because the information is useful and instructional. Because of where this is falling within the book, you may not understand many of the things that I'm going to talk about. I suggest that you skim through this section to begin with and then return to it later after you've worked through Chapter 2. The first panel of the Project Settings window, shown in Figure 1.9, shows the general settings for the project. Most of these you won't need to change, with the exception of configuring your source code management by using the Configure Roots and SCM button.
