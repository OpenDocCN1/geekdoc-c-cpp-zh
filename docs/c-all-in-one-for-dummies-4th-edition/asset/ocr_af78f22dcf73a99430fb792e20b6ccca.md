You don't have to type the source code for this chapter manually. In fact, using the downloadable source is a lot easier. You can find the source for this chapter in the \CPP_AIO4\Book1\Chapter03 folder of the downloadable source. See the Introduction for details on how to find these source files.

# Code::Blocks Creating a Project

Creating a computer application is usually a bigger job than you'd want to organize in your head. Application code is saved in files much like the documents in a word processor. But applications often have more than one source-code file. At big companies in big buildings in big cities, some applications are *really* big — hundreds of source-code files for just one application.

# Understanding projects

Applications can contain a lot of source code. To keep all that source code together, programmers use a file that manages it all, called a project. A project has a few key elements:

+   - A set of source-code files
+   - (Optional) Resource information such as icons and sound files
+   - A description of how to compile (build) the application
+   - Integrated Development Environment (IDE) settings that tell how to set up the editor you use to write the application
+   - Some general descriptions of the application being built, such as its name and the type of application it is

The *type* of application doesn't mean “word processor” or “really cool earth-shattering software,” even if that's what your application is. This book uses *type* to mean your application's overall relationship with other applications:

+   - Does this application run by itself?
+   - Does this application add to or extend the functionalities of another application (such as Firefox)?
+   - Does this application serve as a *library* (a bunch of code that you make available to another application)?