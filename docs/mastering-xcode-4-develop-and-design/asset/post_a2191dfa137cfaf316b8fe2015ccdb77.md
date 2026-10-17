
![](img/d4b18a89aece4a6ccac4cb886bdef5f7_162_0.png)

**FIGURE 13.3** The Rename sheet

## MOVE UP/MOVE DOWN

Move Up takes the declaration and implementation of the selected item and moves them to a superclass. Move Down moves the selection to one or more subclasses of the current class.

## ENCAPSULATE

Encapsulate creates accessor methods (getters and setters) for a selected instance variable and changes all direct references to them so the accessors are used instead.

## MODERNIZE LOOP

Modernize Loop converts while or C-style for loops to Objective-C 2.0 for loops.

## CONVERT TO OBJECTIVE-C 2.0

Convert to Objective-C 2.0 modifies the code in the selected source files to take advantage of Objective-C 2.0 features. This includes modernizing loops and converting accessor methods to properties and synthesized accessors.

## USING REFACTOR

To familiarize yourself with the Refactor feature, you can rename the NSTextField outlet you created in Chapter 5 from textField to a more descriptive helloTextField. To begin, open the TestApp project and navigate to the TestAppAppDelegate.m file. Double-click the textField symbol on line 13, and select Edit > Refactor > Rename from the main menu. A sheet will appear similar to **Figure 13.3**. Change the name to helloTextField, and click Preview.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_163_0.png)

**FIGURE 13.4** The Rename preview sheet

Xcode will present a preview sheet similar to Figure 13.4 and analyze your project to locate all references to the symbol. You can use the Rename preview sheet to verify and cherry-pick individual replacements.

You can use the list on the left side of the window to jump directly to each instance that will be renamed. Each item has a check box that lets you choose whether that file will be included in the renaming changes. In this case, there are three files that will be modified: TestAppAppDelegate.h, TestAppAppDelegate.m, and the English version of MainMenu.xib. The right pane shows two versions (“before” and “after”) of the selected file. If you select TestAppAppDelegate.m in the list, you’ll notice two red tick marks in the track of the scroll bar. These indicate the places within the file where the symbol is referenced or defined (where changes will be made). Click Save to make the changes.

If you examine all three files (right-click the text field in the xib to examine its referencing outlets), you’ll notice the change has been applied. You should now be able to build and run the application to test it. Click the Say Hello button to make sure the greeting still appears in the renamed field.

The process is similar for each of the available Refactor actions. Though the preview sheet works the same, the initial sheet (shown in Figure 13.3) will contain the various options available for each action.

> **TIP:** Not all refactoring actions can be carried out without your intervention. The Issues button above the change list can be used to explore any problems that Refactor anticipates with performing the proposed action.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_163_1.png)

## ORGANIZING WITH MACROS

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_164_0.png)

**FIGURE 13.5** The Jump Bar pop-up organized using `#pragma mark`

Xcode includes CPP, the C preprocessor, through which your code is run just prior to compilation. The preprocessor transforms your code wherever macros are encountered. For example, when it encounters an `#import` directive, the preprocessor replaces it with the referenced file (nearly always a header file) so its contents are available to the compiler.

A less obvious use of preprocessor macros is for organization within a graphical editor. Using the `#pragma mark` directive, you can define areas within your source file. When you have this file open in the Source Editor, the last segment of the Jump Bar (which, as you’ll recall, lists class members for easy navigation) will reflect your marks by grouping them in its pop-up menu. For example, **Figure 13.5** shows one possible organization of the TestAppAppDelegate.m file.

To use the directive, just place it (along with a name for the section) on a blank line by itself as follows:

```objc
#pragma mark Constructors / Destructors
```

You can go a step further and place a separating line in the menu by using a dash as the mark as follows:

```objc
#pragma mark -
```

There is no defined standard dictating how you should use this directive, nor does it have any effect on your compiled code (it is not part of the compiled code). Although it’s easy to get carried away and pepper your code with marks, most take a minimalist approach and group methods by their primary function.

As an example, you might create a section for UI actions in a controller class, another section for model manipulation methods, another for initialization and deallocation, and another still for accessors. Figure 13.5 roughly follows this general approach. Your style may vary.

## CHANGING EDITOR KEY BINDINGS

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_165_0.png)

**FIGURE 13.6** The Key Bindings preferences panel

Although the focus of the Key Bindings preferences panel (**Figure 13.6**) is not limited to the Source Editor, it’s worth pointing out that you can customize even the most basic Mac OS text editing and navigating keyboard shortcuts in Xcode 4. Developers familiar with the shortcuts of other environments will find this invaluable.

To open the Key Bindings preferences panel, choose Xcode > Preferences from the main menu and then select Key Bindings from the toolbar. The left side of the panel provides controls for managing command sets you create or customize. The right side lets you locate and customize shortcuts.

The shortcuts are grouped by function in the list. You can filter the list using the search bar at the top. To the left of the search bar, you can choose to show only menu- or text-editing shortcuts.

> **NOTE:** The shortcuts for most any item in Xcode’s menu can be customized (or added if none yet exist). The list of customizable shortcuts is quite extensive and worth a few minutes of your time to browse.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_166_0.png)

## MANAGING COMMAND SETS

You can think of command sets as “keyboard shortcut profiles.” For example, if you were nostalgic (or stubborn), you could create a command set whose text shortcuts match those of Vim or CodeWarrior.

Use the + and - buttons at the bottom of the list to create or remove command sets. Although not really obvious, the currently selected command set is the one currently in effect and is persistent. To switch to a different command set, just select it.

## CUSTOMIZING SHORTCUTS

To customize a shortcut, double-click the field in the Key column next to the shortcut. The field will become highlighted, and + and - buttons will appear near its right side. The - button removes a shortcut, and the + button lets you add shortcuts (so multiple shortcuts can fire the same action). To set a shortcut, press the key combination you’d like and then click outside the field to end editing (or press the + button to add another).

## JUMP TO DEFINITION

The Source Editor hides a simple navigational shortcut you won’t be able to live without once you know it’s there. Although not strictly an editing feature, the need to navigate to the definition of a symbol (possibly one of many) while writing your code is common. Xcode makes this simple. Hold down the Command key and hover the mouse pointer over any symbol to turn the symbol into a hyperlink. Click the link (while still holding down Command) to navigate to the symbol’s definition (or implementation). When multiple definitions exist for the clicked symbol, a pop-up similar to Figure 13.7 appears, listing all known definitions of the symbol (and the file and line number where each appears). Select any definition to navigate to it.

Very few developers are likely to work for a company called “My Company Name,” yet Xcode insists on inserting this in the copyright block at the top of any source files it creates. If you’re not currently employed by My Company Name, it’s wise to change the Organization field associated with the project so the copyright of newly created files reflects your actual organization (or even just your name).

To do this, select the project itself (the top-level object) in the Project navigator; then open the Utility area and select the File Inspector pane. Under the Project Document section, type the name of the desired copyright holder in the Organization field. Any source files Xcode creates from that point forward will insert that name instead of the standard __My Company Name__ placeholder.

## WRAPPING UP

This gentle introduction to the more advanced (or simply less common) aspects of Xcode 4 has given you a handful of powerful Source Editor features. These features offer elegant solutions to tedious and error-prone editing tasks developers encounter often when writing or maintaining code.

In the next chapter, you’ll learn about Xcode 4’s new Schemes system and how to customize the build and archive process, set up target dependencies, and more.
