# Tip

When using the Use Access Special Keys property to disable Access's default accelerator keys, you can still use an AutoKeys macro to set your application's shortcut keys.

# Compact on Close

Checking the Compact on Close check box tells Access to automatically compact and repair your database when you close it. Some Access developers use Compact on Close as a way to perform this maintenance process each time a user works with a database, while others find it unnecessary. We're in the latter camp, but you can decide for yourself based on the level of activity in your database. You must close and reopen the current database in order for this change to take effect.

# NOTE

Access includes a utility named Compact and Repair Database on the Database Tools Ribbon. File-based databases, such as Access, need such a utility to avoid data corruption, optimize performance, and reduce file sizes. As records are added to and deleted from tables, the size of your Access database file can become large. Compacting an Access database forces Access to rebuild the indexes in all the tables, and physically rearranges tables in primary key order in the ACCDB file. The maintenance operations ensure that your Access databases operate at maximum efficiency. Keep in mind that compacting a large database might take a considerable amount of time. Plus, Compact on Close only affects the front-end database. Unless your application uses the front end for temporary tables or other operations that cause the front end to bloat, the Compact and Repair Database option may be of minimal benefit to your users.

# Remove Personal Information from File Properties on Save

Checking this box automatically removes the personal information from the file properties when you save the file. You must close and reopen the current database for this change to take effect.

# Use Windows-Themed Controls on Forms

Checking this box uses your system's Windows theme on the form/report controls. This setting only applies when you use a Windows theme other than the standard theme.

# Enable Layout View

The Enable Layout View check box shows or hides the Layout View button on the Access status bar and in the shortcut menus that appear when you right-click an object tab.