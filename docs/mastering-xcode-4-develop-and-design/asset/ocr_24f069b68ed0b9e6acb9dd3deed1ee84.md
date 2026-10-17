FIGURE 14.11 The Build Settings tab

FIGURE 14.12 A multiple-selection pop-up window

The URL Types section allows you to define URL schemes your application understands. An example might be a URL that takes the form of testapptask://taskid and causes your application to be launched and display the task with the specified taskid. See the Launch Services Programming Guide in Apple’s documentation for more information.

The Services section lets you define system services (such as Insert Employee ID Here), which can be accessed from other applications. See the Services Implementation Guide in Apple’s documentation for more information.

# THE BUILD SETTINGS TAB

The Build Settings tab (Figure 14.11) contains all the build settings for the selected target, grouped by category. The simplest view, as shown in Figure 14.11, can be seen by setting the filter bar (just beneath the tab bar) to show Basic and Combined. This instructs the editor to show you only the most commonly used settings and only the values for the selected target.

For each setting, you can edit the matching value under the column named after your target. Some values are simple strings while others are presented in a pop-up menu. In cases where you can make more than one selection (such as the Architectures setting), you can select Other from the menu and you’ll be presented with a pop-up window (Figure 14.12) that allows you to add multiple selections. In the figure, an environment variable is used that, to Xcode, means the standard 32/64-bit universal binary.