Notice that the “Output location” field contains a path within your user profile. The template itself is a ZIPped archive that is about to be exported into the Visual Studio 10\My Exported Template under your profile’s documents folder.

When you click Finish, the wizard collects all the files to include in the project template and puts them into a zip archive. At the end of the process, the output folder is opened in New Windows Explorer instance, and you can see the Basic Console.zip file there. Open this archive to have a look at it. You will see a folder and four files, as illustrated in Figure 4-8.

![](bbox=[0.5, 0.185, 0.865, 0.273])

In addition to the original files of the project, you should create two new files by wizard—TemplateIcon.ico and MyTemplate.template. Later in this chapter, you’ll learn what these files are and what their roles are in Visual Studio’s infrastructure.

Close the Windows Explorer instance and go back to Visual Studio. The exported template is ready to be consumed. Create new Visual Studio project with the File > New Project command, and scroll down to the bottom of the template list within the Visual C# category. You should see the Basic Console template, as shown in Figure 4-9.

![](bbox=[0.075, 0.508, 0.735, 0.84])

FIGURE 4-9: The template is ready to be consumed.