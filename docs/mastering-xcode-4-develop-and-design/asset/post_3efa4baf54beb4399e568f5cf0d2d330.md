

**FIGURE 16.9** The Schemes pop-up menu showing workspace-wide schemes

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_240_0.png)

## Managing Schemes in Workspaces

You learned the ins and outs of managing schemes in Chapter 14. Here you’ll manage them from another perspective—schemes as they exist within a workspace.

You’ve no doubt noticed schemes from each project show up in the Schemes pop-up in your new TestApp Suite workspace. The schemes are inherited from the workspace projects in which they exist. Figure 16.9 shows the schemes from both the TestApp and TestAppSharedFramework projects.

Choose Manage Schemes from the Schemes pop-up to reveal the now-familiar scheme manager (Figure 16.10). There are two major questions to consider for each scheme in a workspace: Should it be shown, and in what container should it exist?

### Showing and Hiding Schemes

In Figure 16.10, note the Show column in the list of schemes. Though all schemes are visible in the scheme manager, deselecting the Show check box for a scheme removes it from the Schemes pop-up control.

In the TestApp Suite, you have only an application and its shared library. When looking at it from the workspace perspective, it may be necessary to show only the application and the framework schemes. Since the TestAppImporter target that you created earlier is a dependency of the TestApp target, you may not want to bother seeing it from the workspace perspective.

It’s important to note that the Show settings for each scheme persist whether you’ve opened a workspace containing it or the project itself. In other words, if you change this setting for a project’s scheme, the change appears in the workspace (and if you change it in the workspace, it appears in the project’s settings as well).

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_241_0.png)

**FIGURE 16.10** The scheme manager

### Changing a Scheme’s Container

The Container field of the scheme manager indicates where the scheme is stored. This field lets you move schemes by changing their container to another project. When viewing the schemes at the workspace level, you can move schemes to be contained entirely in that workspace. This capability lets you create a shared scheme that builds an entire suite of products from disparate projects with a scheme that only appears when working with the entire workspace.

> **NOTE:** Recall that the scheme manager’s Shared check boxes dictate whether a scheme shows for other users who open the project or workspace. In a team setting, there will likely be at least one shared scheme—the scheme to build them all.

## Another Kind of Workspace

**FIGURE 16.11** The Behaviors panel

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_242_0.png)

The term *workspace* has been overloaded in the software industry. Its meaning in Xcode is no exception. It makes sense that Xcode calls its new feature “workspaces” (a good name for a feature that binds projects together), but in the broader sense, *your workspace* refers more to the layout and configuration of your project.

Your Xcode workspace includes, among other things, controls for whether or not certain auxiliary views are enabled. Xcode 4 helps you maintain control of your workspace by using behaviors. Under Xcode’s Preferences (Command-Comma), the Behaviors panel reveals a number of configurable options (Figure 16.11).

Although there are many options, the feature is simple. Each item in the list on the left can trigger any of the actions on the right. Behaviors affect all projects and workspaces (the bound-together-projects kind). With Lion’s auto-hiding scroll bars, it’s easy to miss, but both the left and right lists are scrollable. Figure 16.11 shows the window large enough to see the contents of both lists without scrolling.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_243_0.png)

**FIGURE 16.12** The Behaviors menu

### Uses for Behaviors

An example of a custom behavior would be to not show the debugger when the app runs (“Run starts”) unless the application generates output (“Run generates output”). Another might be to create a new tab and navigate to the current run log in that tab if the app crashes (“Run quits unexpectedly”). The options are simple and speak for themselves. They allow navigation, activation of the various editing modes and assistant panels, running scripts, and so on.

### Defining Behaviors

Xcode already has a number of common situations in the list on the left side of the Behaviors panel. To configure a behavior for a given situation, select the situation on the left and use the check boxes to enable each custom behavior. Those that are customizable have additional controls to the right of their check boxes. Situations that have defined behaviors have a check mark to the left of their names.

### Creating Custom Behaviors

In Xcode 4.1, Apple has introduced custom behaviors. Although these behaviors aren’t triggered automatically like the built-in ones, you can create them and trigger them via the Xcode application menu (Figure 16.12) or with a custom keyboard shortcut.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_244_0.png)

**FIGURE 16.13** A custom behavior

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_244_1.png)

**FIGURE 16.14** Defining a behavior’s keyboard shortcut

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_244_2.png)

**FIGURE 16.15** A useless bezel alert invoked by a behavior shortcut

To create a new behavior, open the Behaviors panel and click the Add (+) button in the lower-left corner. You can name the new behavior whatever you wish. **Figure 16.13** shows a custom behavior named “Alert Me!” whose only action is “Show bezel alert.”

Double-click the Command symbol (the same symbol you see on your Command key) to the right of the custom action name to assign a custom keyboard shortcut to it. Press the combination of keys, then use your mouse to select another entry and end editing the shortcut. **Figure 16.14** shows the custom action with a new (and hard to press) shortcut.

When you press the keyboard shortcut (while Xcode is active), the bezel alert will appear for a moment (**Figure 16.15**). While unexciting (the bezel alert function only shows the name of custom alerts), it’s easy to see how a simple set of keyboard shortcuts could easily switch your Xcode workspace among a number of different configurations tailored to the task at hand.

## Wrapping Up

The idea of Xcode’s new workspaces feature can seem intimidating at first. You’ve seen that it’s really quite straightforward. A workspace provides a way of tying related projects together to take advantage of Xcode’s (usually) intelligent dependency discovery. In the next chapter, you’ll explore some of Xcode’s more advanced debugging and analysis capabilities.

## 17 Debugging and Analysis in Depth

You scratched the surface of Xcode’s debugging and analysis capabilities in Chapter 9 by looking at the most common features developers are likely to use. In this chapter, you’ll explore another powerful feature—the static analyzer—and then delve deeper into the Debug navigator. After that, you’ll take a close look at the debugger console and some of its useful command-line interface tricks. You’ll round out the tour by learning how to debug iOS applications on the device or by using the iOS Simulator.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_247_0.png)

### Using the Clang Static Analyzer

**FIGURE 17.1** An issue highlighted by the static analyzer

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_248_0.png)

**FIGURE 17.2** A static analyzer issue expanded into steps

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_248_1.png)

LLVM (the modular compiler) provides static analysis functionality via Clang, its C language family front end. The Clang Static Analyzer performs semantic analysis and can find logic problems, memory management errors, dead stores (unused variables), and API usage problems. This functionality is built right into Xcode.

When you invoke Xcode’s Analyze action, the analyzer works to identify problems with your code. If an issue is found, it is flagged in the Source Editor and in the Issue navigator alongside errors and warnings (Figure 17.1). Clicking the issue in the editor or the Issue navigator reveals details about the issue in the editor, including helpful blue lines indicating the problematic code path with descriptions of your errant actions along the way (Figure 17.2).

> **TIP:** The Clang Static Analyzer can be run as a standalone tool, providing textual output of its analysis results. Its integration with Xcode is what provides the much nicer graphical interface.

