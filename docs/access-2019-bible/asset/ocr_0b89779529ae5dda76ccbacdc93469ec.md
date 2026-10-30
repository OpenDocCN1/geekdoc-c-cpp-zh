In the Chapter23.accdb database, start by opening tblProducts in Datasheet view. On the Ribbon, you'll select the Table tab to expose the table's data events (see Figure 23.1). Click the After Update command to open the macro builder (shown in Figure 23.5). Initially, at least, there's not much to look at.

# FIGURE 23.5

The macro builder for the table's AfterUpdate event.

![](bbox=[0.16, 0.37, 0.78, 0.67])

The large blank area to the left is the macro design area. This is where you place macro actions. On the right side is the Action Catalog, a hierarchical list of all macro actions currently available. The only indication of which table event is being programmed is in the main Access window caption and in the tab above the macro design area.

With a macro open in the design area, the Ribbon contains several tools you use when working with the macro. Notice that you can collapse or expand macro sections, save the macro currently under construction, and close the macro builder.

You'll notice that the Ribbon you see in Figure 23.6 is exactly the same seen when working with embedded or standard macros. However, some options are not available to you. All the items in the Tools group, for example, are grayed out. This is because data macros don't provide the option of single-stepping through macro actions or converting to VBA code. Data macros are intended to be relatively simple, short, and to the point, rather than large and complex.