![](bbox=[0.156, 0.077, 0.742, 0.312])

Figure 5.2: New, improved error dialog box

were handling this error allowed the user to proceed with our application and enter new information only to find out they can't save it. With this error message, we stop that from occurring by forcing the user to quit until they deal with the error. The resulting error message is shown in Figure 5.2.

We do have one other addition to this error check. Before we present the NSAlert to the user, we also dump the information about the error to the console. This is primarily useful during the development cycle but can also be helpful when we have a user with an unusual issue. When Core Data fails with more than one error, it will load all the errors into a single NSError instance that it passes back to us. In that situation, the top-level `-localizedDescription` will tell the user only that “Multiple Validation Errors Occurred,” which is not very useful to us as developers. However, the other errors are available for display, we can get them from the `userInfo` of the `NSError`, and we can then iterate over them, print out their `-localizedDescription` to the console, and reveal the exact problems. We also check to make sure there are suberrors so that we can print out the top-level error by itself if there is only one.

# ## 5.2 A Simple Migration

To demonstrate a simple migration, we will add the ability to attribute recipes to authors. To kick off the versioning, the first thing that we