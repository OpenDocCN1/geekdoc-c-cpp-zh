
## PROGRAMMING EXAMPLE: ICW WaterDepth File App

In Chapter 12, a graphical user interface solution was designed to enable users to enter areas along the ICW where boaters were advised to take warning because of shoaling or shallow water. The graphical user interface enabled users to enter a location name, state, mile marker number, and four separate days of water depth at low and high tide. When valid data was entered, a message was displayed showing the location and its associated data. However, after the data about a single location was processed and displayed, it was lost when the second and subsequent locations were entered. There was no mechanism available to store the data from one run to another run. For this programming example, the solution presented in Chapter 12 will be modified to allow the results to be captured and stored for future use.

### ANALYZE THE PROBLEM

You should review the problem specification in Figure 12-21 and make sure you understand the problem definition. Several values must be entered into the program. Instead of allowing a single set of location and associated depths to be entered, the application should allow multiple locations to be entered. A Windows application was developed as part of the solution for the programming example illustrated in Chapter 12. When a Windows application is run, it is put in a process loop and can handle multiple value sets. Minor modifications will be needed to ready the form for the second and subsequent set of input values.

### DATA

Three classes were designed for the solution to the WaterDepth application in Chapter 12. You should review Table 12-4. It lists the data field members needed for the ShoalArea class. No new data members are needed for this class. No changes are needed for the TestOfStateException class. The FrmWaterDepth class created the user interface and displayed a message showing the problem area and its water depths. In this class, an object of the StreamWriter class will be created.

### DESIGN A SOLUTION

Instead of simply displaying a message showing the location of the shoal area and data describing the current condition of the reported problem, the data will be stored in a text file. Depths will be delimited or separated by a comma and a space. The location will be separated by a comma and a space. The state and the mile marker will be followed by a colon, space, and hyphen, respectively. Averages will be stored inside parentheses and inserted following the raw data they are representing. Usually, you do not store calculated values in a data file or database; there is no need to take up additional storage for calculated values because they can be derived at any time using the raw data. Also, storing calculated values can lead to inconsistent data. If one of the day’s depths gets changed and the average does not, the integrity of the data is decreased. Figure 13-15 shows a prototype of what the data file might look like.

![](img/36e48639a06772bcb0fa1ea2525b33a3_915_0.png)

**Figure 13-15** Data file prototype

The first two printed lines would not appear in the file. They are included here to document what the values are. The three lines under Examples are indicative of what the output would look like.

### CODE THE SOLUTION

You may want to look ahead at Figure 13-16 to review the form used to collect the data. The revised source code listings for the ShoalArea and the FrmWaterDepth classes follow.

```csharp
// ShoalArea.cs
// This class defines a ShoalArea location
// where water depths in the ICW are problematic.
// Data stored in a text file includes the
// name of the location, state, mile marker, and
// four days of high and low tide depths, and averages.

using System;
using System.Diagnostics;

namespace WaterDepth
{
    public class ShoalArea
    {
        private string location;
        private string state;
        private double mileMarker;
        private double[] lowTideDepth;
        private double[] hiTideDepth;

        public ShoalArea()
        {
            lowTideDepth = new double[4];
            hiTideDepth = new double[4];
        }

        public ShoalArea(string loc, string st, double mile,
            double[] low, double[] hi)
        {
            location = loc;
            CheckStateOk(st);
            mileMarker = mile;
            lowTideDepth = low;
            hiTideDepth = hi;
        }

        public ShoalArea(string loc, string st, double mile)
        {
            location = loc;
            state = st;
            mileMarker = mile;
        }

        // Properties
        public string Location
        {
            get { return location; }
            set { location = value; }
        }
        public string State
        {
            get { return state; }
            set { CheckStateOk(value); }
        }
        public double MileMarker
        {
            get { return mileMarker; }
            set { mileMarker = value; }
        }
        public double[] LoTideDepth
        {
            get { return lowTideDepth; }
            set { lowTideDepth = value; }
        }
        public double[] HiTideDepth
        {
            get { return hiTideDepth; }
            set { hiTideDepth = value; }
        }
        public double CalculateAverageDepth
            (double[] depthArray)
        {
            double sum = 0;
            double avg;
            try
            {
                foreach (double val in depthArray)
                    sum += val;
                avg = sum / depthArray.Length;
            }
            catch (System.DivideByZeroException e)
            {
                avg = 0;
                Trace.WriteLine("Attempted to Divide by Zero" +
                                "\nException Type: " + e.Message);
            }
            return avg;
        }

        public void CheckStateOk(string st)
        {
            switch (st.ToUpper())
            {
                case "FL":
                case "GA":
                case "NC":
                case "SC":
                case "VA":
                    state = st.ToUpper();
                    break;
                default:
                    TestOfStateException ex =
                        new TestOfStateException
                            ("State not Part of Atlantic ICW");
                    throw ex;
            }
        }

        public string ShoalAreaRecord
        {
            get
            {
                string rec = location + ", " + state.ToUpper() +
                    ": " + mileMarker + ", ";
                foreach (double val in lowTideDepth)
                    rec += val + ", ";
                rec += "(" +
                    CalculateAverageDepth
                        (lowTideDepth).ToString("0.00") + ", ";
                foreach (double val in hiTideDepth)
                    rec += val + ", ";
                rec += "(" +
                    CalculateAverageDepth
                        (hiTideDepth).ToString("0.00") + "; ";
                return rec;
            }
        }

        public override string ToString()
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
}
```

A special property, ShoalAreaRecord, was defined to format the raw data with delimiters. Notice how this property resembles the single data member properties you used previously. The keyword get is followed by statements that concatenate the data fields onto the string that is returned. The object's ToString( ) method is overridden to provide a formatted string for output.

The FrmWaterDepth class follows. New event handlers have been added for the form load and form closing events.

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

        public FrmWaterDepth()
        {
            InitializeComponent();
        }

        private void FrmWaterDepth_Load(object sender, EventArgs e)
        {
            anArea = new ShoalArea();
```
