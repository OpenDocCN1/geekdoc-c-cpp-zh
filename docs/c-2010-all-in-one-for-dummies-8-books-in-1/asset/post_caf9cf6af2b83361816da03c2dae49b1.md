
# 502 Paneling the Studio

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_527_0.png)

**Figure 2-5**
When you use Data View, who needs SQL Management Studio?

## Paneling the Studio

Paneling: That's just so very seventies.

To be as flexible as it needs to, Visual Studio has a large collection of modular windows that are called panels. These panels do everything that isn't involved with directly editing a design or code. They manage files, manage objects, show feedback, preferences, all sorts of stuff.

Visual Studio has something like 23 panels. I don't have room to discuss them all here, I cover only 5 — the ones you use every day. The rest you can find in the View menu.

### Solution Explorer

Solution Explorer (see Figure 2-6) manages solutions, projects, and files. Despite my claim earlier that solutions are just a matter of files and folders, it is a somewhat more complex operation than it seems at first blush.

# Paneling the Studio 503

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_528_0.png)

**Figure 2-6:** The explorer of solutions.

### Solutions

For solutions themselves, Solution Explorer provides a useful interface for what is basically tools, including the following:

- **Configuration Manager** provides a useful interface for what is basically a settings in the solution itself. You can specify whether Release or Debug compilation is desired for your build here, if you want all debugging information stored with your file. You can tell the compiler you want the software built for 32-bit systems or 64-bit systems too.
- **Project Dependencies** shows how your projects are interrelated and describes the way in which your projects depend on each other. It has a tab for the build order, When you are getting weird “referenced member not available in object” errors, check here first.
- **Property Pages** determine which project should start on debug and where source files are kept, among other things.

Additionally, Solution Explorer is a repository for projects. Each appears in a tree view.

### Projects

Projects are the individual compiled units and are divided by type. You can find more about projects in Chapter 1 of this minibook.

Solution Explorer brings to the capability to add and remove files, make references and services, set up a class diagram, open the representative Windows folder, and set properties.

# 504 Paneling the Studio

All this information is saved in the Project file. The project file is just an XML file. There are a few key characteristics of the file:

- It includes a PropertyGroup for each build type. This is because you can set different properties for each type of executable.
- It contains an ItemGroup that has all the references in it, including Framework versions, and another set of ItemGroups that have the project load details.
- The file includes the import of the project general details and the Target collections. You can actually edit the file manually to make a custom build environment.

You likely won't modify your Project file, but I think it's important that you know it can be done, and that Microsoft has inline comments. They expect the file to get hacked.

Files are a less exciting. They are pretty much exactly what you expect. They host the source code of the program being developed. Nothing hidden here.

Solution Explorer manages the files in the project basically like Windows Explorer. Solution Explorer lists the files and folders and allows them to be opened in the designer or the code editor.

Solution Explorer also knows what to show. If the file isn't in the project but happens to be sitting in the folder for the project, it won't show in the Explorer. If you can't find a file, try clicking the Show All Files button in the gray bar at the top of the Explorer. The hidden files will show gray out, but still won't compile into the project.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_529_0.png)

The Properties panel (see Figure 2-7) is a simple, flexible tool that allows you to update these endless lists of details about everything in development projects. The panel is basically a window with a two-column-wide datagrid. It reads properties in key/value pairs for easy view and edit.

When I say it shows endless lists of details about everything, I mean everything. If you click on nearly anything in Visual Studio, press F4 to bring up the Property Panel (refer to Figure 2-7), you will get properties. Try it with these functions:

- In Solution Explorer
- Database connections
- A textbox in a WPF project
- An XML tree node
- An item in Class Explorer

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_530_0.png)

If there is any meta-data about something, the properties are in the Property Panel. It’s a great tool.

## The Toolbox

One of the greatest misunderstood tools is the Toolbox. (See Figure 2-8.) On the surface it seems so simple. The design-time controls for a given file type are available to drag and drop. Still, there is one important thing you need to remember about the Toolbox. Wait, I’ll get out of it.

The Toolbox displays only controls.

# 531

# 506 Paneling the Studio

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_531_0.png)

**Figure 2-8:**
The Toolbox
with tools.

## Server Explorer

Server Explorer (see Figure 2-9) isn't in every version of Visual Studio. At the time this book was printed, it was included only in Professional Edition and later.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_531_1.png)

# Paneling the Studio 507

Server Explorer enables developers to access important services on a remote machine. These could be anything from SharePoint to MSMQ but generally include two types of services:

- Managed services
- Database connections

### Managed services

Managed services are things like Event Viewer and Microsoft Message Queue: things that you would need to look at of your application. Internet Information Services, for example, is a managed service that would show up in the list.

To get a service in Server Explorer, follow these steps:

1. Right-click on Servers.
2. Click the Add Server button.
3. Type the machine name or IP number of the server you want to add.
4. If you want to use different credentials than you used to log in (for a different account, for instance), click Connect Using a Different User Name and enter the new credentials.
5. Click OK.

Play around the services you see. There are a lot of features in this panel that I don't have space to get into here.

### Data connections

Above the Services in Figure 2-9 are the data connections. These are data connections that have been made on previous projects, which Visual Studio keeps around in case you need them for any other projects. Although keeping connections around seems a bit of a security risk, it sure as he is inconvenient.

The goal is to reduce the dependency on SQL Management Console (the old method for managing the database for developers), and it does a darn good job. The key issue is access to the data model (table names and columns and stored procedures; developing a program without access to the data-base is tough).

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_532_0.png)
