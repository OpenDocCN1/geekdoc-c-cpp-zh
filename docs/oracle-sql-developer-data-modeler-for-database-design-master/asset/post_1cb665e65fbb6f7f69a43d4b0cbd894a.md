
## 208 Oracle Developer Data Modeler for Database Design Mastery

Committing Working Copy preference is not needed because of the default behavior of Data Modeler.

- If you select Automatic Locks Files with Sv:needs-lock Property After Check Out, files you check out from the repository are automatically locked. This behavior is not recommended by Subversion, and I suggest you uncheck this preference. Locking makes using the tool more complicated, and the tools works perfectly without locks. As a database person, I wanted to locking, but after selecting it for a while and locking the files from myself, I decided not to use locking and found it more flexible but still a safe way of working. But if you decide to use the locking model of working, remember that a strange locking occurs, there is a way to solve it: Choose Team | Cleanup Working Copy.

- When performing a merge operation, there are two choices: a dialog box or a wizard. If you select the Merge Wizard For Subversion Merge preference, the wizard is used. Otherwise, the Merge dialog box is opened for merge requests.

If you select Show Log Messages In Subversion Console, the SVN Console – Log pane opens automatically when there are log messages to be shown. These messages are about operations between Data Modeler and Subversion when you commit changes. Here's an example:

```
commit - "m -N C:/../rel/62GAAD018-081AFB6E3EE/table/seg_0/
5891AED-CA-75-BB62-C06F-083F1571634.xml
Adding C:/Users/Heli/DMSubversionTestIMall/User2/Design1/
rel/62GAAD018-081AFB6E3EE/table/seg_0/F5891AED-CA-75-BB62-C06F-
083F1571634.xml
Transmitting file data ...
Committed revision 66.
```

Having this preference on all the time might be annoying since you will get a lot of information. You might want to disable it and select it only if for some reason need to debug problems with Data Modeler and Subversion or if you are importing a design to version control. If you change this preference, you need to restart Data Modeler to put the new setting into action.

- In Operation Timeout, you specify the maximum number of seconds, minutes, or hours allowed for a Subversion operation to complete.

- If you want to edit the Subversion configuration file, you can do so by clicking the Edit “Server” button in Edit Subversion Configuration File. Lines beginning with # are comments. If you click Reset, your unsaved changes are removed from the file, and the editor stays open. If you click OK, the changes are saved, and the editor is closed. Cancel cancels all the changes and closes the editor. If your company has strict security settings, you might need to edit the configuration file and add a proxy exception to be able to use version control. You just add the following line in the [global] section: http-proxy-exceptions = *.mycompany.com. Or you might want to edit the Web Browser Proxy preferences.

On the Version Tools tab, you can define the Pending Changes dialog and Merge Editor works. In the Pending Changes dialog, you can see the Outgoing Changes (changes you have made and saved) and Incoming Changes (changes somebody else has made and committed to Subversion). For the Pending Changes Window option, you can specify whether the Outgoing Changes dialog will always be shown, when changes are hidden, or never shown (Using Outgoing Commit dialog). The Incoming Timer preference specifies the time interval for Data Modeler to check the status of files in Subversion for incoming changes. You can manually check the status at any time with the Refresh Incoming Changes preference on the Incoming Changes tab in Pending Changes. You can also define whether the merge will be done locally or at the server by setting the Merge Editor preference. My personal preference is locally so I always know that my local version is the one I want to commit to Subversion.

## Chapter 9: Using Version Control and Working in a Multiuser Environment (Subversion)

### Introducing Subversion

Before you start with Subversion, you must install it. Check in the Preferences dialog to see which version of Subversion is supported by Data Modeler. Download that version of Subversion, follow the instructions, and install it.

If you need Subversion only for version control purposes, the easiest way is to use Oracle SQL Developer to create a local repository. Then you do not need to do anything. In Oracle SQL Developer, choose Team | Subversion | Create Local Repository. Follow the instructions, and you will have a local repository that you can use for version control. If you also need the multiuser environment features, you need to create a real Subversion repository on a server.

When you are working with Subversion, you always have a working copy of your design on your own computer. When you save, you save the changes to copy of the design. When you commit, you bring your changes from the local working copy to the copy in Subversion. Checking out from a Subversion repository creates a working copy of that directory on your computer and the .svn directory. Unless otherwise defined during the checkout, this copy contains the most recent versions of the directory and its tree found in the Subversion repository.

In the working copy directory, there is a directory called .svn that includes files Subversion is using to manage your working copy and to control that everything works as it should. If you accidentally remove the .svn subdirectory or anything else happens to it, the easiest way to fix the problem is to remove all the files and directories and check out the design again. The Subversion server does not know there are working copies on your computer, deleting the working copy does not affect Subversion. But make sure you have committed all the changes before deleting the working copy.

The working model with Subversion is a copy-modify-merge solution. Copy (from the version control to your working directory), modify your copy in the working directory, and merge your changes to Subversion. Each time you commit, you create a new revision of your design to the repository. There is always a number identifying the revision. Each revision number has a file system tree attached to it, which is a snapshot of the moment it was saved. The revision number applies to the whole tree, not individual files.

In Subversion, a project is a solid unit of something like in Modeler. It is a directory under which all the files are saved. In Subversion you can define permissions for user groups and add user accounts to the rights to grant them permissions. But somebody must maintain the hierarchies. The other possibility is to grant privileges to the Subversion repository or to the main data for Modeler designs.

Subversion does not give the structure for your project layout, and it does not define for you whether you need one repository or several repositories. You can have one project per Subversion repository, all your projects in one repository, or something in the middle. If you decide to have one repository, it typically means less administration, but revision numbers are global and cannot be used as meaningful. Large projects can cause problems to other projects in the same repository, for instance, by taking a lot of resources from the repository. Multiple repositories usually work best if the projects have nothing to do with each other and need to be administered separately. In that case, the repository structure can be tailored to each repository and user permissions can be defined easily, but there is a big limitation: Subversion does not support merging between different repositories. In general, the easiest solution is to have one repository for all the Modeler designs.

Subversion does not define the structure of a repository or the project layout. You might want to have three subdirectories in your Subversion repository either in the root or per design directory: trunk, branch, and tags. Trunk is the main line or root of the design, and the main development line should be saved in the trunk folder. You might want to create specific branches, and they should be saved in the branch directory. Tags are named, stable snapshots of a particular line of development and saved in the tags directory. For example, version 1.0 of the design could be saved
