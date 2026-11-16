# # 1 BUILD THE UI

We'll start by building the basic window that contains a DockPanel, a TreeView containing several items at two levels, and a TabControl with one TabItem. If you'd like to use something other than Recipes in your sample, feel free (you could go back to that list of applications you want to write), but for our purposes, you'll want a two-level hierarchy with details to be displayed in tabs.

![](bbox=[0.18, 0.3, 0.62, 0.68])

The TreeView is decked to the left.

Setting LastChildFill to true takes care of the size and position of the TabControl.

This is just a Label inside the TabItem that tells the user what they need to do to display the recipe details.

# ## PUT ON YOUR THINKING HAT

Create a new Visual Studio WPF project and build the basic window as shown.