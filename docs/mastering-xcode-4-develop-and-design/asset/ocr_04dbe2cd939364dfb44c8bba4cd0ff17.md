The clone or checkout will begin. You may be asked for authentication information. Supply the necessary information and click OK to proceed. Depending on the size of your repository, the actual checkout or clone may take a while. When it's finished, it will show up in the Organizer along with the rest of your repositories.

NOTE: It's common to set up an SSH key for “passwordless” authentication to an SCM server. If you have a key set up for the server already and Xcode prompts you for a username and password, it's best to leave the username field as it is and supply no password. For a Git-themed example of setting up an SSH key, see http://xcodebook.com/gitkey.

# PERFORMING ROUTINE SCM TASKS

You've seen how to clone and generally manage your Git repositories. Now you'll explore how to perform the more typical day-to-day SCM management tasks in Xcode and manage changes to your projects.

# MANAGING FOLDERS IN SUBVERSION

Subversion works with files and folders; Git works with files or chunks (changed parts of files). For this reason, Subversion users need to make directory structure changes through Subversion, whereas Git users are able to freely move files and folders around.

In Xcode, you manage Subversion folders using the Repositories tab of the Organizer. You'll need to first select the repository. To add a folder, use the list in the right-hand pane (the one showing your working copy's directory structure) to select a folder in which you want to create the subfolder, then click the New Directory button. To delete a folder, click the Delete button in the Organizer. Rename folders by clicking them in the Organizer and editing them as you would any other filename. Each of these changes will require an immediate commit. Xcode will prompt you to enter a commit message.

![](bbox=[0.78, 0.32, 1.0, 0.48])