```
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace Methods2
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        public void switchToReadingMode()
        {
            readingText.BackColor = Color.Maroon;
            readingText.ForeColor = Color.White;
        }
        private void readingModeButton_Click(object sender,
            EventArgs e)
        {
            switchToReadingMode();
        }
    }
}
```
```

Code 11.14

+   7. Build and run the project. The program window will appear as follows:

![](bbox=[0.4, 0.78, 0.62, 0.88])

Figure 11.6. The initial view of the program

When the Reading mode Button is clicked, our method will be executed and change the colours of the Label: