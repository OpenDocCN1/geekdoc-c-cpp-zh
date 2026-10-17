# EXTENDING YOUR WORKFLOW WITH CUSTOM SCRIPTS

In Chapter 14, you explored Xcode’s redesigned build system. You learned that there are separate build actions that are run against the active scheme. You also learned that the action you perform will automatically build the specified targets in the way that makes the best sense for that action (a build for running yields a Debug build; a build for archiving yields a Release build). Two important features were mentioned briefly: the ability to run scripts before and after each type of action and the ability to run a script as part of a build phase.

# SCRIPTING OPPORTUNITIES

Xcode offers several opportunities to hook in your custom scripts to extend functionality. Xcode has always come with the Run Script build phase (see Chapter 14), but Xcode 4 adds pre- and post-action scripts, which are run before and after each major action (such as Build, Run, Archive, and so on).

# PRE- AND POST-ACTION SCRIPTS

In Chapter 14, you learned about the Run Script build phase, which, as its name suggests, runs the specified script when the target to which it belongs is built. The limitations of such a script are the same as its benefits: It runs only when its target is built. The ability to run a script just before (or after) a Run action, however, would let you reset the application’s test data before launch to always run against the same test data (or clean up a mess after the app finishes running). A bit of postprocessing for an archive created by the Archive action would be helpful for many developers as well. For each build action (Build, Run, Test, Profile, Analyze, and Archive), you can run a custom script before and after. These are called pre-action and post-action scripts.

To manage pre- and post-action scripts, you edit the scheme into which you want to place them. From there, you select the action and expand it by clicking the disclosure button and selecting Pre-actions or Post-actions. Figure 19.1 shows the post-action editor for the Run action of the TestApp scheme.