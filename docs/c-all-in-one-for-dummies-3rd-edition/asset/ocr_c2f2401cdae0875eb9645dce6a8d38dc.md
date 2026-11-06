# ## Understanding projects

Applications can contain a lot of source code. To keep all that source code together, programmers use a file that manages it all, called a *project*. A project has a few key elements:

+   - A set of source-code files
+   - (Optional) Resource information such as icons and sound files
+   - A description of how to compile (build) the application
+   - Integrated Development Environment (IDE) settings that tell how to set up the editor you use to write the application
+   - Some general descriptions of the application being built, such as its name and the type of application it is

The *type of application* doesn’t mean “word processor” or “really cool earth-shattering software,” even if that’s what your application is. This book uses *type* to mean your application’s overall relationship with other applications:

+   - Does this application run by itself?
+   - Does this application add to or extend the functionalities of another application (such as Firefox)?
+   - Does this application serve as a *library* (a bunch of code that you make available to another application)?

All this information, along with your source-code files, represents a project.

In the Code::Blocks IDE, you create a new project each time you start work on a new application. You provide a little information about the application you’re working on, and then you begin writing your code. All the code for your application is stored in one place — in the project.

![](bbox=[0.148, 0.697, 0.233, 0.762])

This book presents a lot of sample applications, so you may want to create a directory (or *folder*) on your hard drive to house all the applications you create as you work through this book. The downloadable source code uses a folder named CPF_AIO. You can read about how to obtain the downloadable source and other extras for this book in the Introduction.

# ## Defining your first project

To create a new project in Code::Blocks, start Code::Blocks and choose File;New;Project, or click *Create a New Project* on the *Start Here* page that appears when you start the application. A dialog box appears, as shown in Figure 2-1.