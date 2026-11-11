![](bbox=[0.364, 0.139, 0.723, 0.323])

**Figure 11.26** A tooltip

| javax.swing.JToolBar | 1.2 |
|---|---|
| • `JToolBar()` | |
| • `JToolBar(String titleString)` | |
| • `JToolBar(int orientation)` | |
| • `JToolBar(String titleString, int orientation)` | constructs a toolbar with the given title string and orientation. orientation is one of `SwingConstants.HORIZONTAL` (the default) or `SwingConstants.VERTICAL`. |
| • `JButton add(Action a)` | constructs a new button inside the toolbar with name, icon, short description, and action callback from the given action, and adds the button to the end of the toolbar. |
| • `void addSeparator()` | adds a separator to the end of the toolbar. |

| javax.swing.JComponent | 1.2 |
|---|---|
| • `void setToolTipText(String text)` | sets the text that should be displayed as a tooltip when the mouse hovers over the component. |

# 11.6 Sophisticated Layout Management

So far we’ve been using only the border layout, flow layout, and grid layout for the user interface of our sample applications. For more complex tasks, this is not going to be enough.