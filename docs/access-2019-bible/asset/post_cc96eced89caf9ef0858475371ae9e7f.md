
# Part VII: Advanced Access Programming Techniques

## Display Form

The form you select in the Display Form drop-down list automatically opens when Access starts the application. When the form loads, the Form Load event of the display form fires (if it contains any code), reducing the need to use an Autoexec macro.

> **TIP**
> 
> Consider using a splash screen as your startup display form. For more information, see the “A splash screen” section later in this chapter.

## Display Status Bar

You can deselect the Display Status Bar check box to remove the status bar from the bottom of the Access screen. (This option is selected by default.)

> **TIP**
> 
> The status bar is an informative and easy-to-use tool because it automatically displays key states (such as Caps Lock and Num Lock), as well as the Status Bar Text property for the active control. Instead of hiding the status bar, you should make full use of it and disable it only if you have a very good reason to do so.

## Document Window Options

Under Document Window Options, you can choose how the forms and reports look in your distributed application. Your options are:

- **Overlapping Windows:** Overlapping Windows retains the look of previous versions of Access, letting you look at multiple forms at once.
- **Tabbed Documents:** Tabbed Documents (the default) uses a single-document interface (shown in Figure 31.2) similar to recent versions of popular web browsers.

You must close and reopen the current database for the changes to take effect.

The Display Document Tabs check box is only available when you select Tabbed Documents; it turns on or off the tabs that appear at the top of any open database object. This setting turns off only the tabs and does not close tabbed objects themselves.

## Use Access Special Keys

If you select this option, users of your application can use accelerator keys that are specific to the Access environment in order to circumvent some security measures, such as unhiding the Navigation pane. If you deselect this option, the following keys are disabled:

- **F11:** Press to show the Navigation pane (if hidden).
- **Ctrl+G:** Press to open the Immediate window in the Visual Basic Editor (VBE).

## Tip

When using the Use Access Special Keys property to disable Access's default accelerator keys, you can still use an AutoKeys macro to set your application's shortcut keys.

## Compact on Close

Checking the Compact on Close check box tells Access to automatically compact and repair your database when you close it. Some Access developers use Compact on Close as a way to perform this maintenance process each time a user works with a database, while others find it unnecessary. We're in the latter camp, but you can decide for yourself based on the level of activity in your database. You must close and reopen the current database in order for this change to take effect.

## NOTE

Access includes a utility named Compact and Repair Database on the Database Tools Ribbon. File-based databases, such as Access, need such a utility to avoid data corruption, optimize performance, and reduce file sizes. As records are added to and deleted from tables, the size of your Access database file can become large. Compacting an Access database forces Access to rebuild the indexes in all the tables, and physically rearranges tables in primary key order in the ACCDB file. The maintenance operations ensure that your Access databases operate at maximum efficiency. Keep in mind that compacting a large database might take a considerable amount of time. Plus, Compact on Close only affects the front-end database. Unless your application uses the front end for temporary tables or other operations that cause the front end to bloat, the Compact and Repair Database option may be of minimal benefit to your users.

## Remove Personal Information from File Properties on Save

Checking this box automatically removes the personal information from the file properties when you save the file. You must close and reopen the current database for this change to take effect.

## Use Windows-Themed Controls on Forms

Checking this box uses your system's Windows theme on the form/report controls. This setting only applies when you use a Windows theme other than the standard theme.

## Enable Layout View

The Enable Layout View check box shows or hides the Layout View button on the Access status bar and in the shortcut menus that appear when you right-click an object tab.

## Enable Design Changes for Tables in Datasheet View

The Enable Design Changes for Tables in Datasheet View check box allows you to make structural changes to your tables in Datasheet view, as opposed to having to be in Design view. In most well-designed Access applications, the users never see the tables in either Design view or Datasheet view, instead interacting with data via forms. If your application allows viewing tables in Datasheet view, you should uncheck this option to prevent unwanted changes to your tables’ designs.

## Check for Truncated Number Fields

Checking this option makes numbers appear as ##### when the column is too narrow to display the entire value. (This behavior has been in Excel for a long time.) Unchecking this box truncates values that are too wide to be displayed in the datasheet, which means that users see only a part of the column’s value when the column is too narrow and might misinterpret the column’s contents.

## Picture Property Storage Format

Under Picture Property Storage Format, you can choose how graphic files are stored in the database. Your options are:

- **Preserve Source Image Format (Smaller File Size):** Choose this option if you want to store the image in the original format, which also reduces the database size.
- **Convert All Picture Data to Bitmaps (Compatible with Access 2003 and Earlier):** Choose this option if you want to store all images as bitmaps, which increases the database size but keeps it compatible with previous versions of Access (Access 2003 and earlier).

You have the option to Preserve Source Image Format to conserve disk space by reducing the database file’s size. (This option is only available in the ACCDB file format.) When using this option, Access only stores one copy of an image (in its original format) and dynamically generates a bitmap when the image is displayed on a form or report.

## Navigation options

The settings in the Navigation section let you define parameters that affect how users navigate your database as an application.

## The Display Navigation Pane check box

With most distributed applications, you might never want your users to have direct access to any of your tables, queries, forms, or other database objects. It’s far too tempting for a user to try to “improve” a form or report or to make some minor modification to a table or query. Rarely are users really qualified to make such changes to an Access database. Deselecting the Display Navigation Pane option hides the Navigation pane from the user at startup.

> **NOTE**
> 
> Unless you also deselect the Use Access Special Keys option (described earlier in this chapter), users can press F11 to unhide the Navigation pane.

You must close and reopen the current database for this change to take effect.

## The Navigation Options button

One nice addition to recent versions of Access is the ability to select which database objects are exposed to users when the Navigation pane is visible at startup. Clicking the Navigation Options button opens the Navigation Options dialog box (shown in Figure 31.3), which you use to change the categories and groups that appear in the Navigation pane.

## FIGURE 31.3

The Navigation Options dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1043_0.png)

In the Grouping Options section, click a category on the left side of the dialog box to change the category display order or to add groups to the right side of the dialog box. Click the Object Type category to disable viewing of certain Access objects (tables, queries, forms, reports, macros, or modules).

In the Display Options section, you can select the Show Hidden Objects, Show System Objects, and Show Search Bar check boxes.

> NOTE
> It's usually a good idea to hide the hidden and system objects, which you normally don't want to modify. (They're hidden for a reason!)
> The Search Bar (shown in Figure 31.4), on the other hand, is useful in the Navigation pane when you have a lot of objects and want to narrow the list to avoid excessive scrolling, so you should select the Show Search Bar check box. For example, if you wanted to see the objects (tables, forms, etc.) that had the word Product in them, you'd type Prod in the Search Bar to limit the tables shown in the Navigation pane.

## FIGURE 31.4

The Search Bar appears at the top of the Navigation pane.

![](img/1e45673ab6eca9d20e67635ff5b9b318_1044_0.png)

In the Open Objects With section of the dialog box, select Single-Click or Double-Click to choose how you open a database object. Double-Click is the default option and is most likely familiar to all your users.

## Ribbon and toolbar options

The settings in the Ribbon and Toolbar Options section let you define custom Ribbons and toolbars when using your database as an application. All the options in this section require you to close and reopen the current database for the change to take effect.

Creating custom Ribbons is explained in Chapter 30.
