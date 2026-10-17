![](bbox=[0.135, 0.17, 0.56, 0.295])

FIGURE 21.16 The branch selection sheet

Enter your commit message in the text editor at the bottom of the sheet, and click the Commit button to commit the changes. Assuming there were no errors, the SCM status flags will then disappear, showing that there are no files with outstanding SCM status.

> NOTE: When you use the main File menu to commit changes to projects across multiple repositories, Xcode treats this as if you'd performed individual commits for each working copy or clone using the same commit message.

If you need to commit only a handful of files, you can select them individually in the Project navigator, right-click one of the selected files, and choose Source Control > Commit Selected Files from the context menu. The same commit sheet you saw in Figure 21.15 will appear, and it works the same way. You can also commit from the Repositories tab of the Organizer by selecting a working copy or clone from the source list and pressing the Commit button on the bottom toolbar.

# PUSHING CHANGES

When using a Git repository cloned from a remote origin, you can also use the Source Control menu to push your local commits to the origin from within Xcode. Choose File > Source Control > Push from the main menu. A sheet will appear (Figure 21.16), asking you to choose the branch to which to push. Once you choose the branch, click Push. Xcode will then push the changes.

![](bbox=[0.75, 0.42, 1.0, 0.565])