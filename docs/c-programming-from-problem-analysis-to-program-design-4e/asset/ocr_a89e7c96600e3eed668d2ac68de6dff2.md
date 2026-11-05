```
```csharp
public override string ToString( )
{
    return "Location: " + location +
        "\nState: " + state +
        "\nMile: " + mileMarker +
        "\nAverage Low Water Depth: " +
        CalculateAverageDepth(lowTideDepth).ToString
        ("F2") + "\nAverage High Water Depth: " +
        CalculateAverageDepth(hiTideDepth).ToString
        ("F2") + "\nOverall Average Water Depth: " +
        ((CalculateAverageDepth(lowTideDepth) +
        CalculateAverageDepth(hiTideDepth))
        / 2.0).ToString("F2");
}
}
```
```

A special property, ShoalAreaRecord, was defined to format the raw data with delimiters. Notice how this property resembles the single data member properties you used previously. The keyword get is followed by statements that concatenate the data fields onto the string that is returned. The object's ToString( ) method is overridden to provide a formatted string for output.

The FrmWaterDepth class follows. New event handlers have been added for the form load and form closing events.

```
```csharp
// FrmWaterDepth.cs
// This class defines the Graphical
// User Interface class. Values retrieved
// from the user are stored in a text file.

using System;
using System.Windows.Forms;
using System.Diagnostics;
using System.IO;

namespace WaterDepth
{
    public partial class FrmWaterDepth : Form
    {
        private ShoalArea anArea;
        private StreamWriter file;

        public FrmWaterDepth( )
        {
            InitializeComponent( );
        }

        private void FrmWaterDepth_Load(object sender, EventArgs e)
        {
            anArea = new ShoalArea( );
```
```