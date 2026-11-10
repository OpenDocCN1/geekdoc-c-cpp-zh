
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_74_0.png)

Figure 2.14 Creating a Request

## 2.4 Summary

In this chapter, we explored the technical aspects of an SAP system. Even though SAP Basis administrators perform most of the setup and configuration for the components discussed in this chapter, having a basic understanding of these components helps when developing ABAP programs.

We discussed the three layers of an SAP system—namely, the presentation layer, application layer, and database layer. We also explored the different components that make up these systems, such as different SAP GUI versions and the components of the application server and database server.

We also looked into the client concept and discussed the data structure of an SAP system and how the data can be made specific to a client or available across clients.

Finally, we provided an overview of repository objects and how they're grouped into packages. This overview lays the foundation to discuss development objects.

In the next chapter, we'll begin to introduce you to the ABAP environment and the ABAP Workbench tools.

## 3 Introduction to the ABAP Environment

Now that you’ve walked through the SAP system, let’s turn our attention to the ABAP environment. In this chapter, we’ll introduce native IDE and the Eclipse IDE plug-in.

SAP provides an integrated development environment (IDE) called *ABAP Workbench*, a collection of tools used to develop, test, and run ABAP programs. After the release of SAP NetWeaver 7.31 SPS 4, SAP introduced the *ABAP Development Tools* (ADT) for SAP NetWeaver, also known as *ABAP in Eclipse*, which adds Eclipse capabilities to ABAP Workbench (Transaction SE80) functionality.

In this chapter, we will showcase SAP GUI and the Eclipse IDE and introduce the ABAP Workbench tools that we’ll use to develop various ABAP programs throughout this book.

In Section 3.1, we’ll begin by looking at the SAP environment in general, including information on the ABAP programming environment and steps for logging onto the SAP system. We’ll also look at the different elements of an SAP screen and how to use transaction codes to get from point A to point B.

Section 3.2 will dig into the different ABAP tools found in ABAP Workbench. This includes the ABAP Editor, Function Builder, Class Builder, Screen Painter, Menu Painter, ABAP Data Dictionary, and Object Navigator. Each of these tools will be used and discussed throughout the remainder of the book, so it’s important to gain a good understanding of their functions and purpose.

We’ll end the chapter with an overview of the Eclipse IDE in Section 3.3, including steps for installation and setup.

### 3.1 SAP Environment

As discussed in earlier chapters, you can use SAP GUI or a web browser (SAP Web GUI for traditional applications or for Web Dynpro applications) to logon to an SAP system and run applications. However, ABAP Workbench tools are fully supported in a desktop environment for both SAP GUI and Eclipse IDE. To avoid confusion and to follow a consistent theme throughout the book, we will be using SAP GUI for Windows in this book for all examples. You should be able to use SAP GUI for Java or Eclipse IDE to follow the examples without any difficulty.

In this section, we'll explain how to logon to an SAP system and navigate through the SAP screens. We'll explore the different ways to run SAP applications and will look at various elements of an SAP screen.

**3.1.1 ABAP Programming Environment**

Unlike in other programming languages (Java, C/C++, etc.), ABAP source code is not stored in files; instead, all ABAP source code is saved in the underlying database of the SAP instance. There is no separate compiler for ABAP code; the ABAP runtime environment itself interprets and executes ABAP code.

The database interface in the work process communicates with the underlying database. The database interface converts Open SQL statements in the ABAP program to Native SQL statements (native to the underlying database). The ABAP runtime system ensures that the ABAP programs are operating system- and database-independent, making ABAP programs portable. In other words, you don't have to worry about changing your program code if the underlying database or operating system environment changes.

In the next few sections, we'll explore these environments and their on-screen elements in greater detail.

**3.1.2 Logging On to the SAP Environment**

The SAP logon screen shows four input fields, as shown in Figure 3.1. Along with username (User) and Password, you also enter the ID of the Client you wish to logon onto. SAP supports multiple languages, so you can choose a LOGON LANGUAGE from any of the installed languages in your SAP system.

To use a specific language, input its two-digit SAP language code on the logon screen—for example, “EN” for English, “DE” for German, and so on. The logon screen also includes a New Password button to change your password.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_78_0.png)

**Figure 3.1** SAP Logon Screen

Once you fill in the details on the logon screen, press `Enter` to log on to the system.

**3.1.3 Elements of the SAP Screen**

Upon successful logon, you'll see the default SAP Easy Access screen (see Figure 3.2); this entry screen is always displayed after logon and is used for opening various SAP applications. The SAP Easy Access screen includes a customizable SAP menu with a tree structure in which all the installed applications are organized into various folders.

The navigation area of the SAP Easy Access screen is divided into the SAP Menu, User Menu, and Favorites:

- **SAP Menu**：The SAP Menu is delivered standard with SAP.
- **User Menu**：The User Menu can be customized to display user-specific applications based on the user's role in the organization. For example, a finance user might see finance-related applications and a sales user may see sales-related applications by default in the SAP Menu.
- **FAVORITES**：Frequently accessed applications can be added as favorites under the Favorites folder for quick access.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_79_0.png)

**Figure 3.2** SAP Easy Access Screen with Screen Elements

[Figure 3.2](#) shows the various screen elements of a standard SAP screen as accessed by the SAP GUI.

Now, let's walk through each of the standard screen elements identified in [Figure 3.2](#).

**Menu Bar**

The menu bar is where various menu items for applications are located. You can use the menu bar to carry out additional activities with the application. When developing your own ABAP applications, you can design the menu bar by using the Menu Painter tool (Transaction SE41). You'll learn more about Menu Painter in Section 3.2.5 and how to use it in Chapter 12.

The menu bar consists of an application-specific menu, system menu, and help menu. The application-specific menu consists of menu items that are specific to each application and are created when developing the application. For example, if you want the user to download report output to a spreadsheet, you can add a menu item and related functionality to do so. The system menu and help menu are available by default and consist of standard system functions and links to help resources, respectively.

**Standard Toolbar**

The standard toolbar contains a standard set of icons for every application. The standard icons include Save, Back, Exit, Cancel, Print, Find, Find Next, and so on.

You can’t remove icons from or add icons to this toolbar. However, you can enable or disable certain icons for your application according to your business requirements. The standard toolbar is customized via the Menu Painter tool during application development.

**Title Bar**

The title bar displays the title of the application, allowing you to identify the application you're running easily. Based on the type of program, the title is displayed either from the program attributes or from your program code, using the ABAP keyword `SET TITLEBAR`.

You'll learn more about setting the application title and using the ABAP keyword `SET TITLEBAR` in [Chapter 12](#chapter-12).

**Application Toolbar**

The application toolbar displays all the application-specific icons. The application toolbar is located directly below the title bar. This area can be used to provide various icons that enhance the functionality of the application.

It's standard design practice to use an application toolbar to duplicate functions from the menu bar. This allows for quick access to some of the most commonly used functions for the current screen and system task. The buttons available in the application toolbar change from application to application as per each application's design.
