# 638 Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

| 15.1 Introduction | 15.9 TreeView Control |
| 15.2 Menus | 15.10 ListView Control |
| 15.3 MonthCalendar Control | 15.11 TabControl Control |
| 15.4 DateTimePicker Control | 15.12 Multiple Document Interface (MDI) Windows |
| 15.5 LinkLabel Control | 15.13 Visual Inheritance |
| 15.6 ListBox Control | 15.14 User-Defined Controls |
| 15.7 CheckListBox Control | 15.15 Wrap-Up |
| 15.8 ComboBox Control | |

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# # 15.1 Introduction

Here we outline our Forms presentation. We start with, which present users with logically organized commands (or options). We show how to create menus in the Windows designer. We discuss how to input and display times using the MonthCalendar and DateTimePicker controls. We introduce LinkLabels that can link to a file on the current machine or a web page, by simply clicking the control.

We demonstrate how to manage values using a ListBox and ListView to combine several checkboxes in a CheckListBox. We also create drop-down lists using ComboBox and display data hierarchically with a TreeView control. You will learn two important GUI tab controls and multiple document interface (MDI) windows. These components enable you to create real-world programs with sophisticated GUIs. You will use inheritance to build upon an existing GUI.

Visual Studio provides many GUI controls, several of which are discussed in this (and the previous) chapter. You can also design custom controls and add them to the ToolBox, We demonstrate this in this chapter last example. The techniques presented here provide the framework for creating more substantial GUIs and custom controls.

# # 15.2 Menus

Menus provide groups of related commands for Windows Forms apps. Although these commands depend on the program,such as Open and Save—are common to many menus. Menus are an integral part of GUIs, because they organize commands without "cluttering the GUI.

In Fig. 15.1, an expanded menu from Visual Studio lists various controls (called menu items), plus submenu (within a menu). The top-level menus appear in the left portion of the figure, whereas any submenu or menu items are displayed to the right. The menu that contains a menu item is a parent menu. A menu item that contains a submenu is considered to be the parent of that submenu.

Menus have Alt shortcuts (also called access shortcuts, keyboard shortcuts or hotkeys). They are access by pressing Alt and the underlined—forexample, Alt + F typically displays the File menu. Menu items can have shortcut keys as (combinations of Ctrl, Shift, Alt, F1, F2, letter keys, and so on). Some menus display checkmarks, usually indicating that multiple options on the menu can be selected at.