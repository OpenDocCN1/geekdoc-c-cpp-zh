# Chapter 9: Using Version Control and Working in a multiuser Environment (Subversion) 223

![](bbox=[0.118, 0.105, 0.881, 0.463])

**Figure 9-5. A conflict**

be solved by the person who committed last. Conflicts are shown in red in Pending Changes. Solving a conflict must be done manually; it cannot be done automatically. In real life, you cannot have a pattern solution for every conflict.

When a conflict arises, you can see both incoming and outgoing changes at the same time. If you accept the changes made to version control, you simply commit the incoming changes and get those updated to your working copy. You can select the change from the list, right-click it, and choose either Update or Update All. Or you can click the Update Working Copy icon or the arrow beside it and select Update All. Then you decide what to do with the outgoing changes: commit or revert. Remember, everything in red is still in conflict and must be solved before you can continue.

If you do not want to accept the changes committed by somebody to version control, you see them one by one (double-click the change in Incoming Changes) and merge them as you want by clicking Merge (XML Metadata Comparator). Clicking Merge brings the selected to your local working copy. This way, you build the version wanted piece by piece in your local working copy and finally commit it to Subversion as it is.