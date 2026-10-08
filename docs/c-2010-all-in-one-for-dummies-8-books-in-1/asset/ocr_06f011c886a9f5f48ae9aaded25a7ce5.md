# 490 Breaking Down the Projects

Projects are where you put the code files for your programs. They store all kinds of things, like references to the .NET Framework, resources like graphics, and what file should be used to start the project.

Solutions do the same for projects projects do for files. They keep the projects in a folder, and store certain properties. For instance, they store which project should be started when debugging tasks.

Neither the project nor the solutions have much to do with a finished program. They are just simple organizational structures for Visual Studio. The installation of finished program is determined by the setup project. The solution itself is a logical storage mechanism for the source files.

In reality, the solution is more than a folder. A file in a folder that is used by Visual Studio to manage the developer experience. So, inside the folder for the file is describing the projects within, and then a bunch of files with the projects themselves.

There are files for the projects, too — files that describe the resources and references for your project. They are all XML files that contain text references to the values that you set using Visual Studio.

When developing in Visual Studio, you shouldn't worry about that. In 14 years of working in various versions of Visual Studio, I have had to look at a solution or project file only a few times, and only in special situations. Knowing how they work, however, will help you design your project structure.

The way I work is to look at what I want to be a finished program and consider it a solution. Above that, I have a client folder. The result looks like Figure 1-3.

| Client |
| Solution (an application for a client) |
| Project (part of the application, like the user interface) |
| Project |
| Project |
| Solution |
| Project |
| Project |
| Client |
| Solution |
| Project |
| Project |
| Project |

Figure 1-3: My preferred project structure.