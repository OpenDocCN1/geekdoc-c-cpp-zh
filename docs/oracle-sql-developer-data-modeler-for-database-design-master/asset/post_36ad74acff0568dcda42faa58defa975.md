
## Chapter 2: Getting Started with Oracle SQL Developer Data Modeler 13

![](img/431f8ac8f273fa89a28377c500ed60d7_39_0.png)

> **TIP** Choose File | Exit to quit Data Modeler and close all the designs that are open. Data Modeler will ask you to save them all. If you click the Close (X) button in the upper-right corner of the window, you'll be asked if only one of the designs should be saved.

In the Browser pane you can select an entity or a table, right-click, and select Go To Diagram. You will see all the designs, subviews, displays where this object is located and can select the one you want. The diagram/subview/display will open, and the object will be selected on the canvas.

If you right-click the canvas, you will see a few options. You can add to or remove objects from this diagram/subview/display by choosing Add/Remove Objects and deselecting the include property. With Details, you can adjust what object details be shown in the diagram and what will not be shown. And with Show, you can add a grid, a page grid, labels, and legends to the diagram. Grids will help you align the objects and make the diagram easier to read. The page grid shows where a page starts and ends. Labels are, for instance, foreign keys names or source and target names in relationships. The legend shows audit information, including the name of the diagram, author, created time, modified time, design name, and type of model (logical or relational), for example.

If the Browser pane (or any other pane) appears, you can restore it from the View menu. If you need to view the logs in order to troubleshoot something or to know what the tool is, choose View | Log or choose View | External Log depending on which one you need.

The best way to learn how to use the tool is to view the start page (earlier in 2-1). On the start page, you will find links to documentation, tutorials, and online demonstrations. If the start page disappears for some reason, you can get help by choosing Help | Start Page. In fact, you can use the search and table of contents to find more information about the tool. From Help | About, you can check which version and build of Data Modeler you are using. You can also see what components, properties, and extensions are included.

You can use the Navigator pane (on the right of Figure 2-1) to go to an exact point of the diagram or see the whole picture of. The Navigator pane is useful especially if you have a big diagram or you cannot find the object wanted by looking at the canvas. In Navigator, you can drag a red rectangle around the picture. When you move your cursor, the diagram in the logical or relational model moves accordingly. There are also diagrams with toolbars and icons for designing. By right-clicking an object, you can see the operations allowed on that object.

## Oracle SQL Developer Data Modeler for Database Design Mastery

object has properties, and they can be accessed either by right-clicking the object and selecting Properties or double-clicking the object.
There is also a Messages (on the bottom of Figure 2-1) that shows messages about what is happening in Data Modeler. Messages in red might need your attention; anything else is just for your information.
For version control, there is a Versions pane that serves as a Subversion directory and a Pending Changes pane so you can see the incoming and outgoing changes.

## Customizing the Interface

You can customize the Data Modeler user interface depending on how you like to work. Decide which tools will be shown in the screen, you can resize them, and you can move the different panes to different places to serve better. Just drag any panel to move it to the place you want. You will see a rectangle following the pane. When the position and shape is what you want, release the mouse button to drop it. The possibilities are endless, so find a combination that works for you. In Figure 2-2, you can see the way I prefer Data Modeler to be set up to be able to work efficiently.

![](img/431f8ac8f273fa89a28377c500ed60d7_40_0.png)

FIGURE 2-2. My preferred layout for Data Modeler

## Chapter 2: Getting Started with Oracle SQL Developer Data Modeler 15

## Tuning Oracle SQL Developer Data Modeler

Before starting to use Data Modeler in production or in a multiuser environment, it is important to set up the tool in the best way to serve your organization’s needs. You could leave all the preferences at their defaults, but in time you’ll find that you work in a certain way and the settings should reflect that. In the beginning, you should define at least some preferences and design-level properties and maybe create some glossaries and domains. You should also decide where those settings will be kept (preferably in version control) and how they will be shared with other users.

The tool also has design rules to help you maintain the quality of your designs. There are predefined design rules, but you can create as many of yours as needed. Having all this will increase your productivity and the quality of your work.

## Setting Preferences

Preferences are settings that affect Data Modeler behavior on installation level, and you can share these preferences with other Data Modeler installations. Some preferences take effect immediately, but other preferences require you to close the design and reopen it for them to take effect. This is because either the preference is in cache memory or it has been copied to another property elsewhere in a design by Data Modeler. Since the new preference will affect only the elements created after the change, it is important to set your preferences before starting to use Data Modeler. To be sure that a change is really taking effect in the design you open, you can close and reopen the design after changing a preference. Sometimes it is better to even close Data Modeler and reopen it.

In every new version of Data Modeler there are new preferences for the users to tune the tool to fit their needs. See Help on Data Modeler for more specific descriptions of a certain preference. This chapter will cover the most important preferences for a user when using the tool. Other chapters will cover the preferences that affect that particular phase of database design.

You can find the preferences by choosing Tools | Preferences, as shown in Figure 2-3. These preferences have an effect on only your installation of Data Modeler unless you share them with other users, as explained later in this chapter.

## Preferences for Starting to Use Oracle SQL Data Modeler

This section will cover the preferences that will make the tool behave the way you want, and it will explain how to share those preferences with other users after implementing them. You can change all the preferences while working on a project,

## Oracle SQL Developer Data Modeler for Database Design Mastery

![](img/431f8ac8f273fa89a28377c500ed60d7_42_0.png)

FIGURE 2-3. Tools | Preferences

but it is always difficult to change settings later because it will affect all the users and possibly the way tools behave.

Figure 2-4 shows the Preferences dialog, which opens after you choose Tools | Preferences, with Data Modeler selected on the left. Defining the default directories for Data Modeler to use is valuable. It is easier for you to find the directories if you know exactly where they are. You should define the directories on the Data Modeler tab for all your users because it will make your life much easier, especially with version control and problem solving.

- Default Designs Directory is the directory where you will find your designs by default, and if you export or import a Data Modeler design, it will be saved here by default.
- Default Import Directory is the default directory for preferences and design-level property imports, among others.

## Chapter 2: Getting Started with Oracle Developer Data Modeler 17

![](img/431f8ac8f273fa89a28377c500ed60d7_43_0.png)

FIGURE 2-4. Data Modeler Preferences

- Default Save Directory is the directory where you will save files by default. For example, Data Modeler will try to find exported files here by default.
- Default System Types Directory is the directory where all the Data Modeler system files are stored by default. Typically these files are type definition files, default domain files, glossary files, RDBMS sites, customized scripts, and saved search criteria. These files affect your installation of Data Modeler only. Note that for domains, Data Modeler
