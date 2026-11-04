![](bbox=[0.14, 0.1, 0.85, 0.25])

# 15.1	Introduction

Here we continue our Windows Forms presentation. We start with menus, which present users with logically organized commands (or options). We show how to create menus in the Windows Forms designer. We discuss how to input and display dates and times using the MonthCalendar and DateTimePicker controls. We also introduce LinkLabels that can hyperlink to a file on the current machine or a web page, simply by clicking the mouse.

We demonstrate how to manipulate lists of values via ListBox and ListView and how to combine several checkboxes in a CheckedListBox. We also create drop-down lists using ComboBoxes and display data hierarchically with a TreeView control. You'll learn two other important GUI elements—tab controls and multiple document interface (MDI) windows. These components enable you to create real-world programs with sophisticated GUIs. You'll use visual inheritance to build upon an existing GUI.

Visual Studio provides many GUI components, several of which are discussed in this (and the previous) chapter. You also can design custom controls and add them to the ToolBox, as we demonstrate in this chapter's last example. The techniques presented here form the groundwork for creating more substantial GUIs and custom controls.

# 15.2	Menus

Menus provide groups of related commands for Windows Forms apps. Although these commands depend on the program, some—such as Open and Save—are common to many apps. Menus are an integral part of GUIs, because they organize commands without "cluttering" the GUI.

In Fig. 15.1, an expanded menu from Visual Studio lists various commands (called menu items), plus submenus (menus within a menu). The top-level menu appears in the left portion of the figure, whereas any submenus or menu items are displayed to the right. The menu that contains a menu item is called that menu item's parent menu. A menu item that contains a submenu is considered to be the parent of that submenu.

Menus can have Alt key shortcuts (also called access shortcuts, keyboard shortcuts or hotkeys), which are accessed by pressing Alt and the underlined letter—for example, Alt + F typically expands the File menu. Menu items can have shortcut keys as well (combinations of Ctrl, Shift, Alt, F1, F2, letter keys, and so on). Some menu items display checkmarks, usually indicating that multiple options on the menu can be selected at once.