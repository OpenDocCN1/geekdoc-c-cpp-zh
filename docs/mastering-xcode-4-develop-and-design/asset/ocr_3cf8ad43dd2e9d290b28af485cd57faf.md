All is not lost. You can still take full advantage of Git by using the command line to turn an existing project into a Git repository. In the terminal, type the following (where your_project_folder is the full path to your project's main folder):

```
cd your_project_folder
git init
```

That’s it. The folder is now the home of a Git repository, albeit one in which nothing is yet committed.

To create a locally hosted Subversion repository, you can’t use Xcode, but you can use the terminal:

```
svnadmin create your_project_folder
mkdir your_project_folder
```

You can then manually import an existing project into the new repository using the following code:

```
svn import path_to_existing_files file://full_path_to_project_
→ folder/trunk/ -m "Initial import"
```

Not as elegant as Git, but it gets the job done.

# ADDING REPOSITORIES MANUALLY

You can add repositories and working copies with the Organizer. Whether you removed them yourself or Xcode could not for some reason add them automatically when opening a project under version control, you can add and remove them manually. This is done with the Add (+) button at the bottom of the source list.

Keep in mind that the source list is an outline. The top-level nodes are individual repositories. Their children are all the known working copies or clones that belong to them, as well as convenient folders to access branches and tags.