onto the string that is returned. The object’s `ToString( )` method is overridden to provide a formatted string for output.

The `FrmWaterDepth` class follows. New event handlers have been added for the form load and form closing events.

```
```csharp
// FrmWaterDepth.cs
// This class defines the Graphical
// User Interface class. Values retrieved
// from the user are stored in a text file.

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
using System.IO;

namespace WaterDepth
{
    public partial class FrmWaterDepth : Form
    {
        private ShoalArea anArea;
        private StreamWriter fil;

        public FrmWaterDepth( )
        {
            InitializeComponent( );
        }

        private void FrmWaterDepth_Load(object sender, EventArgs e)
        {
            anArea = new ShoalArea( );

            try
            {
                /// To append data onto the end of the file,
                /// as opposed to creating a new file,
                /// add true as the 2nd argument
                //fil = new StreamWriter("WaterData.txt", true);

                fil = new StreamWriter("WaterData.txt");
            }
```
```