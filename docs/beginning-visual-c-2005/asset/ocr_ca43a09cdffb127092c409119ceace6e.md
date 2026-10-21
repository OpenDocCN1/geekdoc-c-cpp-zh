# # Programming with Visual C++ 2005

This uses a .NET library function to write the information between the double quotes to the command line, so this is the CLR equivalent of the native C++ statement that you added to Ex1_01:

```
std::cout << "Hello world!\n";
```

It is more immediately apparent what the CLR statement does than the native C++ statement.

# ## Setting Options in Visual C++ 2005

There are two sets of options you can set. You can set options that apply to the tools provided by Visual C++ 2005, which apply in every project context. Also, you can set options that are specific to a project and determine how the project code is to be processed when it is compiled and linked. Options are set through the Options dialog box that’s displayed when you select Tools > Options from the main menu. The Options dialog box is shown in Figure 1-20.

![](bbox=[0.05, 0.58, 0.95, 0.82])

Clicking the plus sign (+) for any of the items in the left pane displays a list of subtopics. Figure 1-20 shows the options for the General subtopic under Projects and Solutions. The right pane displays the options you can set for the topic you have select in the left pane. You should concern yourself with only a few of these at this time, but you’ll find it useful to spend a little time browsing the range of options available to you. Clicking the Help button (with the ?) at the top right of the dialog box displays an explanation of the current options.

You probably want to choose a path to use as a default when you create a new project, and you can do this through the first option shown in Figure 1-20. Just set the path to the location where you want your projects and solutions stored.

You can set options that apply to every C++ project by selecting the Projects and Solutions > VC++ Project Settings topic in the left pane. You can also set options specific to the current project through the Project > Properties menu item in the main menu. This menu item label is tailored to reflect the name of the current project.