4. As soon as the project is shared, you'll notice some subtle differences in the way the project is visualized in the PROJECT EXPLORER. As you can see in Figure 4.38, each project artifact is now annotated with icons and tags that illustrate its status within the repository. This is a convenient way of keeping track of in-flight changes as you're modifying and/or enhancing the project. Aside from these minor UI changes, it's basically business as usual from an Eclipse perspective.

![](bbox=[0.14, 0.26, 0.49, 0.47])

Figure 4.38 Visualization Differences for Shared Projects in Eclipse

# 4.3.6 Checking in Changes

In order to maintain the integrity of artifacts within the repository, Git does not automatically commit changes to the database. Indeed, when we shared our project with Git, all we really did was place the project files in a directory that Git happens to care about. At this point, Git is generally aware of the files' existence but chooses to ignore them until someone comes along and explicitly tells it to start tracking specific files. In Git terminology, such a command moves the files into the repository staging area (or index).

Once a file is moved into the staging area, it's ready to be committed to the repository database. Of course, even at this point we could still decide to change our mind and revert the file. This two-phase commit protocol ensures that changes to files don't ever accidentally make their way into the database; if a change gets added, it's because someone explicitly staged it and then pulled the trigger to commit it after the fact.