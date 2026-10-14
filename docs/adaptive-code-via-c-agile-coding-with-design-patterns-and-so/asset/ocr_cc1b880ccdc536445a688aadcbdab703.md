class at the time of this writing.

# Cloning a repository

The first step is to clone a repository. All Git commands are provided as parameters to the git command-line application. The clone command requires the address of a repository to clone. The following command clones the repository for this book into a local repository. Remember that Git is distributed source control, so many repositories can exist. You will have full read access to the remote repository but will only be able to write to your own local clone.

Click here to view code image

```
git clone https://github.com/garymcleanhall/AdaptiveCode.git
```

This command creates a new directory called AdaptiveCode under the current working directory. By default, the master branch is selected. Each of the samples in this book are, however, located on different branches, so you need to be able to switch branches.

# Switching to a different branch

After cloning a new repository, change the directory to your local clone by using the change directory command.

```
cd AdaptiveCode
```

The currently selected branch is the default, which for this repository is master. There is not much on the master branch for this repository. Instead, the code is located on other branches. Initially, only the master branch is replicated locally. The rest of the branches are still remote. To view which branches are available locally, supply git with the branch command.

```
git branch
```

This lists only the master branch. To list all of the branches that are available remotely, add the remote switch to the branch command.

```
git branch --remote
```

This lists all of the branches that are available in this repository. Note that all of the branches start with the prefix origin/, which specifies the remote location on which these branches reside. Each repository can have multiple remotes, with origin being the name designated for the remote from which this local repository was cloned.

As a personal preference, I have prefixed every branch with a chX- short code (although branch names can be pretty much anything). This indicates the chapter number to which the branch relates. The rest of the branch name is a more free-form description of its content. Appendix B provides a reference of code listings as they correspond to branch names. Now, by using the checkout command, you can create a local version of the remote branch and move onto it.

Click here to view code image

```
git checkout ch9-problem-statement
```

This creates a local version of the remote branch origin/ch9-problem-statement and alters the current working directory so that the changes present on that branch are brought in. If you list the