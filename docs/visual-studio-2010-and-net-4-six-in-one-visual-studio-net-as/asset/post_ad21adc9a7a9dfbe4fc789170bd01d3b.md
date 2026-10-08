
# Looking into the .vsettings Files

By now, you can imagine what kind of settings are stored in a .vsettings file. This file has an XML format (unfortunately its schema is not published), and looking into it gives you hints about how Visual Studio stores the settings you've saved. The following code snippet is extracted from a .vsettings:

```xml
<UserSettings>
<ApplicationID version="10.0"/>
<ToolOptions>
  <ToolOptionsCategory name="Environment" RegisteredName="Environment">
    <ToolOptionsSubCategory name="Documents" RegisteredName="Documents" PackageName="Visual Studio Environment Package">
      <PropertyValue name="ShowFilesProject" value="true"/></PropertyValue>
      <PropertyValue name="AutoLoadExternalChanges" value="false"/></PropertyValue>
      <PropertyValue name="ChangeDocumentSettings" value="true"/></PropertyValue>
      <PropertyValue name="SaveAsUncodeWhenDataLoss" value="true"/></PropertyValue>
      <PropertyValue name="InitializeFromFileCurrentDocument" value="true"/></PropertyValue>
    </PropertyValue>
    <PropertyValue name="ResaveSavedActiveWindow" value="false"/></PropertyValue>
    <PropertyValue name="DetectChangesOutsideIDE" value="true"/></PropertyValue>
    <PropertyValue name="DontShowGlobalUndoChangeLossDialog" value="true"/></PropertyValue>
    <PropertyValue name="AllowEditingReadOnlyFiles" value="true"/></PropertyValue>
    <PropertyValue name="DocumentDocPreference" value="0"/></PropertyValue>
    <PropertyValue name="MisProjectPathSavesLastItems" value="0"/></PropertyValue>
  </ToolOptionsSubCategory>
  <ToolOptionsSubCategory name="FindAndReplace" RegisteredName="FindAndReplace" PackageName="Visual Studio Environment Package">
    <PropertyValue name="ShowingMessages" value="true"/></PropertyValue>
    <PropertyValue name="InitializeFromEditor" value="true"/></PropertyValue>
    <PropertyValue name="MessageBoxes" value="true"/></PropertyValue>
    <PropertyValue name="HideWindowAfterMatchQuickFindReplace" value="false"/></PropertyValue>
  </ToolOptionsSubCategory>
</ToolOptionsCategory>
</ToolOptions>
<!-- ... -->
</UserSettings>
```

If you look closely, you can recognize several categories, pages, and settings in the Options dialog. The <ToolOptions>, <ToolOptionsCategory>, and <ToolOptionsSubCategory> elements form the hierarchy within the Options dialog. <PropertyValue> elements define settings you can manage in a page.

You can find the .vsettings files for predefined profiles in the Visual Studio 2010 installation directory in the Common\IDEProfiles folder. You should take the time to examine these files to get more information about settings.

# REDUCING EFFORTS WITH KEYBOARD SHORTCUTS

Visual Studio has many commands that you can start from the menus or toolbars of the IDE. Although, you can launch all commands by moving the mouse pointer and clicking the appropriate menu or toolbar item, in many cases, this may be so disturbing that you must interrupt your work. For example, when you edit code and to comment out a block of instructions, you must follow these steps:

- 1. Even if the caret is at the beginning of the block to uncomment, you must move the mouse to the caret position, click the left mouse button, and hold down while selecting the whole text.
- 2. Move your mouse over the Edit menu item, and click on it.
- 3. Move the Advanced item in the Edit menu, and move the mouse over it (or click it). The Advanced menu items are displayed on the screen.
- 4. Click the Command Selection item.

The real issue with these steps is that you must raise your hand from the keyboard, find the mouse, look at the screen, and press mouse several times; if you are interrupted in your typing of code.
You are not allowed to use the mouse! Press the Shift+down arrow keys and keep them pressed while all the lines to comment are selected. Then, simply press Ctrl+K and Ctrl+C, and you are ready. There is no need to remove your hand from the keyboard, and no need to use the mouse. Ctrl+K, Ctrl+C sequence is a shortcut to the Edit+ Command Selection.

This was just a simple example of how useful keyboard shortcuts work. Many commands have shortcuts associated with them. You may find some of them easy to remember, while some of them are difficult to use — depending on how often and in what context you use them.

The IDE allows full control over the keyboard shortcuts assigned to commands. You can tailor them to fit your needs and reduce the efforts required to carry out the most frequently tasks.

## Commanding and Command Contexts

There are many commands available in Visual Studio 2010. You can imagine how difficult it is to find a keyboard shortcut for each of them (and even more challenging to learn by heart). There is no reason to make this full mapping, because many commands are rarely used. If you counted the commands you frequently use while working in the IDE, you'd end up with a few commands, but no more. By Pareto's principle, you should assign shortcuts to the most frequently used commands to improve your productivity by 80 percent.

![](img/b5597c749e848b27b0d305153ae16106_196_0.png)

> *During installation, Visual Studio 2010 applies a default shortcut combination scheme, depending on the settings you have selected. Visual Studio 2010 also includes six other keyboard mapping schemes, each of which differs from the others in the shortcut key combinations assigned by default to UI elements. For a list of these combinations, organized by mapping scheme, see “Pre-defined Keyboard Shortcuts” at http://msdn.microsoft.com/en-us/.*

Commands in Visual Studio are tightly coupled with command targets (entities that know how to interpret a command). For example the Cut, Copy, and Paste commands work differently in different contexts. If you are in the text editor, the Copy command copies the selection. If you use the WPF designer, the currently selected object is copied. The text editor and the WPF designer are both command targets, and they know what to do when the command is sent.

Visual Studio uses a routing algorithm to forward commands to command targets. Instead of getting into all the nitty-gritty details of this algorithm, this discussion simply provides a high-level overview.

In the route to find its target, the command bubbles up from level to level. The active command scope has the chance to handle the command or to refuse it, then the bubble goes on. The routing algorithm defines the following scopes from the roots to the root:

- Present Add-ins and special extensions (Visual Studio Packages) scope — Commands first are offered to the registered and loaded add-ins, or specially registered Visual Studio Packages.
- Context (shortcut) menu — If the user uses a command from a context menu, the command target belonging to this menu has the first chance to handle the command. If it does not, then the normal route (starting from Present-Add-Ins) is.
- Focus scope — The window having is the next entity that could undertake command. This could be a tool window or a document window. The management of the command is different depending on what kind of window is focused.
- Document window scope — Document windows are composed logically from two separate parts: the document view that is responsible for displaying the UI representing the document, and a document data object that is responsible for handling the information before the document. Both the document and the document view can be managed. The command first goes to the data if the view does not support it.
- Tool window scope — A tool window can handle the command with its own logic. There are tool windows that route the commands within them to nested command targets. The Solution Explorer window is an example of this. Within Solution Explorer, a command is routed through the hierarchy composed of the elements of the Solution Explorer where each node has the capability to handle the command. This internal route also goes from the lower hierarchy levels up to the upper levels.
- Current project scope — The current project gets the command. If it does not handle it, the command goes up in the hierarchy of projects to the level of solution. All nodes on this node can manage the command just like other command target objects.
- Global scope — If a command is not handled during the previous levels, the environment attempts to route it to the appropriate package (Visual Studio extension). If necessary, Visual Studio loads the appropriate package into memory.
