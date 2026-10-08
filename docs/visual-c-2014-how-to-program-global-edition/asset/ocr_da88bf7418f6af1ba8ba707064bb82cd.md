# 686 Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

Note the title bar in Fig. 15.40(b) is Form1 - [Child1]. When a window is maximized, its title-bar is inserted into the parent window's title bar. When a child is minimized, its title-bar displays a restore icon, which can be used to return the child window to its size (size before it was minimized or maximized).

C# provides a property that helps track child windows are open in an MDI container. Property MdiWindowListItem of class MenuStrip specifies which, if any, displays a list of open windows that the user can select to bring the corresponding window to the foreground. When a new child window is opened, an entry is added to the end of the list (Fig. 15.41). If ten or more child windows are open, the list includes More Options..., which allows the user to select a window from a dialog.

# Good Programming Practice 15.1

In an MDI app, include a menu that displays a list of the open windows. This helps the user select a child window quickly.

![](bbox=[0.143, 0.355, 0.857, 0.815])

MDI containers allow you to organize the placement of its child windows. The child windows in an MDI app can be arranged by calling method LayoutMdi of the parent Form. Method LayoutMdi takes an enumeration, which allows ArrangeIcons, Cascade, TileHorizontal and TileVertical. Tiled windows completely fill the parent and do not overlap; such windows can be arranged horizontally (TileHorizontal) or vertically (TileVertical). Cascaded windows (value Cascade) overlap - each is the same size and displays a visible title bar, if possible. Value ArrangeIcons arranges the icons for minimized windows. If minimized windows are scattered around the parent window, value ArrangeIcons orders them neatly at the bottom-left corner of the parent window. Figure 15.42 illustrates the uses of the Mdi layout.

Fig. 15.41 | MenuStrip property MdiWindow.MdiListItem example.

ClassUsingMDIForm (Fig. 15.43) demonstrates MDI windows. ClassUsingMDIForm uses three instances of child ChildForm (Fig. 15.44), each containing a PictureBox that displays an image. The parent MDI Form contains a menu enabling users to create and arrange child Forms.