The Tile Horizontal menu item (tileHorizontalToolStripMenuItem) has an event handler (tileHorizontalToolStripMenuItem_Click, lines 65-69) that arranges the child windows in a horizontal manner. The event handler calls method LayoutMdi with the argument TileHorizontal from the MdiLayout enumeration (line 68).

Finally, the Tile Vertical menu item (tileVerticalToolStripMenuItem) has an event handler (tileVerticalToolStripMenuItem_Click, lines 72-76) that arranges the child windows in a vertical manner. The event handler calls method LayoutMdi with the argument TileVertical from the MdiLayout enumeration (line 75).

# MDI Child Form

At this point, the app is still incomplete—we must define the MDI child class. To do this, right click the project in the Solution Explorer and select Add > Windows Form.... Then name the new class in the dialog as ChildForm (Fig. 15.44). Next, we add a PictureBox (displayPictureBox) to ChildForm. In ChildForm's constructor, line 16 sets the title-bar text. Lines 19-21 retrieve the appropriate image resource, cast it to an Image and set displayPictureBox's Image property. The images that are used can be found in the Images subfolder of this chapter's examples directory.

```
// Fig. 15.44: ChildForm.cs
// Child window of MDI parent.

using System.Drawing;
using System.Windows.Forms;

namespace UsingMDI
{
    public partial class ChildForm : Form
    {
        public ChildForm(string title, string resourceName)
        {
            // Required for Windows Form Designer support
            InitializeComponent();

            Text = title; // set title text

            // set image to display in PictureBox
            displayPictureBox.Image =
                (Image)(Properties.Resources.ResourceManager.GetObject(
                    resourceName));
        }
    }
```

Fig. 15.44 | Child window of MDI parent.

After the MDI child class is defined, the parent MDI Form (Fig. 15.43) can create new child windows. The event handlers in lines 18-48 create a new child Form corresponding to the menu item clicked. Lines 22-23, 33-34 and 44-45 create new instances of ChildForm. Lines 24, 35 and 46 set each Child's MdiParent property to the parent Form. Lines 25, 36 and 47 call method Show to display each child Form.