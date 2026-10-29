# Chapter 25: Working with the Schematic View

# Tip

For some relationships, you can double-click on the relationship line to open a dialog box where you can edit the relationship. For example, double-clicking on a Parameter Wire relationship line opens the Parameter Wiring dialog box.

The lower section of the Display Floater lets you show or hide entities that are displayed as nodes, including Base Objects, Modifier Stack, Materials, and Controllers. The P, R, and S buttons let you turn on Positional, Rotational, and Scale controllers. When a node has a relationship with another node, the right end of the node displays an arrow. Clicking this arrow toggles the relationship lines on and off.

The Expand button shows the actual nodes when enabled but only an arrow that can be clicked on to access the nodes if disabled. The Focus button shows all related objects as colored nodes, and all other nodes are unshaded.

Figure 25.7 shows a Schematic View with the Base Objects and Controllers Entities selected in the Display floater. The Expand button is also disabled. This makes up and down arrows appear above each node. Clicking the up arrow collapses the node, rolling it up into its parent. Clicking the down arrow expands the node and displays the Base Object and Controller nodes for the node that you clicked on, such as the Earth node in Figure 25.7. You can also expand and collapse nodes with the Display ▷ Expand Selected and Collapse Selected menu commands.

# FIGURE 25.7

Schematic View nodes can be collapsed or expanded by clicking the up and down arrows.

![](bbox=[0.023, 0.501, 0.598, 0.713])

Collapse (up) arrow

Expand (down) arrow

Hierarchical relationships are shown as lines that connect the nodes. Even if the nodes are moved, the lines follow as needed to show the relationship between the nodes.

# Connecting nodes

To create a hierarchy, use the Edit ▷ Connect (or press the C shortcut) menu command or click the Connect button on the Schematic View toolbar. This enters Connect mode, which lets you link objects together; copy modifiers, materials, or controllers between nodes; or even wire parameters.