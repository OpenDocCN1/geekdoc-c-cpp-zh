# 15.13 Visual Inheritance

Chapter 11 discuss how create classes via inheritance. We've also used inheritance to create Forms that display a GUI, by deriving our New class from class System.Windows.Forms.This is an example of visual inheritance. The derived class inherits the functionality of its Base class, including any base-class properties, methods, variables and controls. The derived class inherits all visual aspects—such as sizing, component layout, spacing between GUI components, colors and fonts.

Visual inheritance enables you to achieve visual consistency. For example, you could define a Base Form that contains a product's logo, a specific background color, a predefined menu bar and other elements. You could then use the Base Form throughout an app for uniformity and branding. You can also create controls that inherit from other controls. For example, you might create a custom UserControl (discussed in Section 15.14) that's derived from an existing class.

# Creating a Base Form

Class VisualInheritanceBaseForm(Fig. 15.45) derives from Form. The output depicts how the Forms works. The GUI contains two Labels with text Bugs, Bugs, Bugs and Copyright 2017, by Deitel & Associates, Inc., as well as one Button that displays the text More. When a user presses the Learn Button, method learnMoreButton_Click (lines 18–24) is invoked. This method displays a MessageBox that provides some informative text.

```
// 15.45: VisualInheritanceBaseForm.cs
// Base Form for use with visual inheritance.
using System;
using System.Windows.Forms;

namespace VisualInheritanceBase
{
    // Base Form used to demonstrate visual inheritance
    public partial class VisualInheritanceBaseForm : Form
    {
        // constructor
        public VisualInheritanceBaseForm()
        {
            InitializeComponent();
        }

        // display MessageBox when Button is clicked
        private void learnMoreButton_Click(object sender, EventArgs e)
        {
            MessageBox.Show(
                "Bugs, Bugs, Bugs is a product of deitel.com",
                "Learn More", MessageBoxButtons.OK,
                MessageBoxIcon.Information);
        }
    }
}
```

Fig. 15.45 | Base Form for use with visual inheritance. (Part I of 2.)