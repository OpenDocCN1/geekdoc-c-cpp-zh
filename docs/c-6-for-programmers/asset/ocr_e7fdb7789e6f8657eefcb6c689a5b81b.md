| MDI parent and MDI child properties, a method and an event | Description |
|---|---|
| **Common MDI Child Properties** | |
| IsMdiChild | Indicates whether the Form is an MDI child. If true, Form is an MDI child (read-only property). |
| MdiParent | Specifies the MDI parent Form of the child. |
| **Common MDI Parent Properties** | |
| ActiveMdiChild | Returns the Form that's the currently active MDI child (returns null if no children are active). |
| IsMdiContainer | Indicates whether a Form can be an MDI parent. If true, the Form can be an MDI parent. The default value is false. |
| MdiChildren | Returns the MDI children as an array of Forms. |
| **Common Method** | |
| LayoutMdi | Determines the display of child forms on an MDI parent. The method takes as a parameter an MdiLayout enumeration with possible values ArrangeIcons, Cascade, TileHorizontal and TileVertical. Figure 15.42 depicts the effects of these values. |
| **Common Event** | |
| MdiChildActivate | Generated when an MDI child is closed or activated. |

Fig. 15.39 | MDI parent and MDI child properties, a method and an event.

Child windows can be minimized, maximized and closed independently of the parent window. Figure 15.40 shows two images: one containing two minimized child windows and a second containing a maximized child window. When the parent is minimized or closed, the child windows are minimized or closed as well.

Parent window icons: minimize, maximize and close

Maximized child window icons: minimize, restore and close

![](bbox=[0.18, 0.73, 0.85, 0.9])

Minimized child window icons: restore, maximize and close

Parent title bar indicates maximized child

Fig. 15.40 | Minimized and maximized child windows.