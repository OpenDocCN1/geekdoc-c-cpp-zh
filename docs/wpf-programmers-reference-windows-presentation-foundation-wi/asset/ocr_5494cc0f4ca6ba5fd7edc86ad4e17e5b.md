When it is displaying the window's controls, this area shows the hierarchical arrangement of controls. For example, Figure 3-27, the window contains a Grid named OuterGrid, which contains two Grids named VBHGrid and InnerGrid. Those controls contain bunch of others. (The squares around a control's type means it has no name).

One of the most confusing uses of this area is how you select controls. If you click on a control, it turns gray and is selected for property editing, so what you make to the Properties apply to the control. In Figure 3-27, the Label that says "Image Brush" is selected for property editing.

If the control you click is a container, it is also highlighted with a blue box. If the control is not a container, then its container is highlighted. In Figure 3-27 the StackPanel containing the Label is highlighted.

If you double-click on a control in the Toolbox, a new instance of that control is highlighted with the blue box. In Figure 3-27, if you double-click the Button tool, a new Button would be added to the highlighted StackPanel.

The Objects and Timeline area has two useful icons to the right of each. The first, which looks like an eye, lets you make the control visible or invisible. Even if you want a control to be visible at run, it's sometimes useful to hide it at design time to reduce clutter so it's easier to see the controls.

The second icon looks like a dot or a padlock depending on whether you have clicked it. When the padlock is visible, the control's properties are locked so you cannot accidentally change them, for example, by dragging the control on the Window Designer.

The Objects and Timeline area has several other features. You can click-and-drag controls to new positions within a container. For example, that would reorder the controls in a StackPanel. It also lets you change the stacking order the controls are painted in order listed first drawn.

One final trick is worth mention here. If you select a group of controls, right-click on them, and select "Group Into," then Expression Blend lets you select a container such as a Grid or StackPanel. When you pick a container, Expression Blend moves the controls that you selected into a new instance of the container.

# Storyboards

In addition letting you edit controls, the Objects and Timeline area lets you build storyboards that control property animations.

To create a storyboard, click on the plus sign at the top of the area. Give the storyboard a descriptive name and click OK.

![](bbox=[0.703, 0.099, 0.915, 0.372])

FIGURE 3-27

Objects and Timeline