+   Trusted Add-In Catalogs: The Trusted Add-In Catalogs section allows you to add, remove, or modify the SharePoint catalogs you trust.

+   Add-ins: Lets you set up how Access handles add-ins. You can choose whether add-ins need to be digitally signed from a trusted source and whether to display a notification for unsigned add-ins. You can also choose to disable all add-ins, which may impair functionality.

+   ActiveX Settings: Lets you set the security level for ActiveX controls.

+   Macro Settings: Lets you set the security setting for macros not in a trusted location. (For more information on Macro Settings, see the previous section on sandbox mode.)

+   Message Bar: Lets you set whether to display the message bar that warns you about blocked content, or to never show information about blocked content.

+   Privacy Options: Lets you choose how Microsoft Office Online communicates with your computer. You can set options to use Microsoft Office Online for help, show featured links at startup, download files to determine system problems, and sign up for the Customer Experience Improvement Program.

# Multi-action Macros

The true power of macros comes from performing multiple actions at the click of a button. Creating a macro that runs a series of action queries is better than double-clicking each action query in the Navigation pane—you may forget to run one or you may run them out of proper sequence.

For this next example, Chapter22.accdb contains two delete queries that remove data from two different tables: tblContacts_Backup and tblProducts_Backup. Chapter22.accdb also includes two append queries that copy records from tblContacts and tblProducts to the backup tables.

The mcrBackupContactsAndProducts macro (also found in the Chapter 22.accdb sample database) automates the running of these four queries so that we have the ability to back up the data in the tblContacts table and the tblProducts table.

Table 22.1 shows the macro actions and action arguments for mcrBackupContactsAndProducts (a portion of which is shown in Figure 22.8).

> NOTE
> If all the actions don't appear in the Action drop-down list, click the Show All Actions command in the Show/Hide group on the Macro Tools Design tab of the Ribbon. Some macro actions require a trusted database or enabling macros through your security settings. Also, some macro actions are considered unsafe because they modify data in the database or perform actions that may cause damage to the application if used incorrectly. Macro actions that are considered unsafe are indicated by a warning icon (which looks like a yellow triangle containing an exclamation point) in the macro designer. By default, Access only displays trusted macro actions that run regardless of the security settings.