```
```csharp
// Fig. 15.48: VisualInheritanceTestForm.cs
// Derived Form using visual inheritance.
using System;
using System.Windows.Forms;

namespace VisualInheritanceTest
{
    // derived form using visual inheritance
    public partial class VisualInheritanceTestForm :
        VisualInheritanceBase.VisualInheritanceBaseForm
    {
        // constructor
        public VisualInheritanceTestForm()
        {
            InitializeComponent();
        }

        // display MessageBox when Button is clicked
        private void aboutButton_Click(object sender, EventArgs e)
        {
            MessageBox.Show(
                "This program was created by Deitel & Associates.",
                "About This Program", MessageBoxButtons.OK,
                MessageBoxIcon.Information);
        }
    }
}
```
```

![](bbox=[0.236, 0.545, 0.663, 0.804])

Fig. 15.48 | Derived Form using visual inheritance

If a user clicks the Learn More button, the event is handled by the base-class event handler learnMoreButton_Click. Because VisualInheritanceBaseForm uses a private access modifier to declare its controls, VisualInheritanceTestForm cannot modify the