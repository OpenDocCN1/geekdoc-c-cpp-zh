FIGURE 16.9 The Schemes pop-up menu showing workspace-wide schemes

![](bbox=[0.281, 0.168, 0.608, 0.315])

# MANAGING SCHEMES IN WORKSPACES

You learned the ins and outs of managing schemes in Chapter 14. Here you'll manage them from another perspective—schemes as they exist within a workspace.

You've no doubt noticed schemes from each project show up in the Schemes pop-up in your new TestApp Suite workspace. The schemes are inherited from the workspace projects in which they exist. Figure 16.9 shows the schemes from both the TestApp and TestAppSharedFramework projects.

Choose Manage Schemes from the Schemes pop-up to reveal the now-familiar scheme manager (Figure 16.10). There are two major questions to consider for each scheme in a workspace: Should it be shown, and in what container should it exist?

# SHOWING AND HIDING SCHEMES

In Figure 16.10, note the Show column in the list of schemes. Though all schemes are visible in the scheme manager, deselecting the Show check box for a scheme removes it from the Schemes pop-up control.

In the TestApp Suite, you have only an application and its shared library. When looking at it from the workspace perspective, it may be necessary to show only the application and the framework schemes. Since the TestAppImporter target that you created earlier is a dependency of the TestApp target, you may not want to bother seeing it from the workspace perspective.

It's important to note that the Show settings for each scheme persist whether you've opened a workspace containing it or the project itself. In other words, if you change this setting for a project's scheme, the change appears in the workspace (and if you change it in the workspace, it appears in the project's settings as well).