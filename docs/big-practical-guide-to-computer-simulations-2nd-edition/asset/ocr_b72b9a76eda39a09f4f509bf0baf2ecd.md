In this example, the files (and all subdirectories recursively) of the directory list are put into a repository directory, which will be created automatically. Here, the repository directory has the same name as the imported directory, but they can have different names. It is also possible to specify the repository without subdirectory (file:///home/hartmann/svn/repos1/). On the other hand, you can also specify a longer pathname if necessary. All directories and subdirectories in the repository are automatically created, if they do not exist. When directly listing the content of a repository using standard operating system commands, you will not be able to see the files or directories you have put in. They are stored internally.

Note that if you do not specify the -m option, subversion will call an editor, where you have to enter a message.

An import command is issued only once for each top-level repository directory. For later changes you have to use the commands commit, add, or remove, see below. Remember always that all files and subdirectories of the given directory are imported. Hence, you should have a clean directory, when you perform an import. For a programming project, for example, this means there should be no object files .o or auxiliary files present.

With the list command, you can view the content of the repository or of subdirectories. Each time only one directory level is shown:³

```
Gene:se>svn list file:///home/hartmann/svn/repos1/
list/
Gene:se>svn list file:///home/hartmann/svn/repos1/list
list.c
list.h
list_main.c
list_mergesort.c
list_remove_element.c
```

Before you start editing some files the first time, you should first checkout the current revision of the project to create a working copy. This starts a so-called working cycle. This is done using the checkout command. As second argument, again the URL of the repository path has to be specified:

```
Gene:listtest>svn checkout file:///home/hartmann/svn/repos1/list
A list/main.c
A list/list.h
A list/list_remove_element.c
A list/list_mergesort.c
A list/list.c
Checked out revision 1.
```