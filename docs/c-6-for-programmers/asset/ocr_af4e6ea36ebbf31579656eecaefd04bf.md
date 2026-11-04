# a) ArrangeIcons

![](bbox=[0.2, 0.2, 0.45, 0.45])

# b) Cascade

![](bbox=[0.52, 0.2, 0.78, 0.45])

# c) TileHorizontal

![](bbox=[0.2, 0.52, 0.45, 0.75])

# d) TileVertical

![](bbox=[0.52, 0.52, 0.78, 0.75])

# Fig. 15.42 | MDI Layout enumeration values.

# MDI Parent Form

Figure 15.43 presents class UsingMDIForm—the app’s MDI parent Form. This Form, which is created first, contains two top-level menus. The first of these menus, File (fileToolStripMenuItem), contains both an Exit item (exitToolStripMenuItem) and a New sub-menu (newToolStripMenuItem) consisting of items for each type of child window. The second menu, Window (windowToolStripMenuItem), provides options for laying out the MDI children, plus a list of the active MDI children.

```
```csharp
// Fig. 15.43: UsingMDIForm.cs
// Demonstrating use of MDI parent and child windows.
using System;
using System.Windows.Forms;

namespace UsingMDI
{
    // Form demonstrates the use of MDI parent and child windows
    public partial class UsingMDIForm : Form
    {
        // constructor
        public UsingMDIForm()
        {
            InitializeComponent();
        }
    }
}
```
```

# Fig. 15.43 | Demonstrating use of MDI parent and child windows. (Part 1 of 3.)