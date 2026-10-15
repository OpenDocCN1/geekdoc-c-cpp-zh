# Immediate Solutions

# Using Graphics in Windows Forms

In the In Depth section of this chapter, you learned about graphics in Windows Forms. You also learned about the different classes that help in creating graphics in Windows Forms. You can use the CreateGraphics() method to create graphics in Windows. The Pen class is used to draw the graphics. The Brush and Color classes are used to fill colors in the shapes created in the Windows Form. Let's use graphics in a Windows Forms application. To do this, create a Windows Forms application named UsingGraphics (also available in CD) and add two Button controls to the Form1 form (Figure 12.3). You can change the text that appears on the Button controls from the Properties window. We have changed the text of button1 to Shape and button2 to Color, as shown in Figure 12.3:

![](bbox=[0.18, 0.29, 0.77, 0.59])

Figure 12.3: Adding Buttons to Form1

Now, add the code, given in Listing 12.1, to the Form1.cs file:

# Listing 12.1: Creating Graphics

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace UsingGraphics
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            Graphics g = this.CreateGraphics();
```