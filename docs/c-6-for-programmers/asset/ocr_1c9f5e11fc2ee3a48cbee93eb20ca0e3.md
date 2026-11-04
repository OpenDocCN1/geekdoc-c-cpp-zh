# ### 21.6.3 Asynchronously Downloading an Image’s Bytes

Method `imagesListBox_SelectedIndexChanged` (lines 99–115) is declared async because it awaits an *asynchronous* download of a photo. Lines 104–105 get the URL property of the selected ListBox item. Then lines 108–109 invoke `HttpClient`’s `GetByteArrayAsync` method, which gets a byte array containing the photo. The method uses the URL specified as the method’s string argument to request the photo from Flickr and returns a `Task<byte[]>`—a *promise* to return a `byte[]` once the task completes execution. The event handler then awaits the result. When the Task completes, the await expression returns the `byte[]`. Line 112 creates a `MemoryStream` from the `byte[]` (which allows reading bytes as a stream from an in-memory file), then line 113 uses the `Image` class’s static `FromStream` method to create an Image from the byte array and assign it to the PictureBox’s Image property to display the selected photo.

# ### 21.7 Displaying an Asynchronous Task’s Progress

Our last example shows how to display an asynchronous task’s progress and intermediate results. Figure 21.6 presents class FindPrimes, which asynchronously determines whether each value from 2 up to a user-entered value is a prime number. During the asynchronous testing of each value, we update a TextBox with each prime that’s found and update a ProgressBar and Label to show the percentage of the testing that has been completed so far.

```
```csharp
// Fig. 21.6: FindPrimes.cs
// Displaying an asynchronous task's progress and intermediate results
using System;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace FindPrimes
{
    public partial class FindPrimesForm : Form
    {
        // used to enable cancellation of the async task
        private bool Canceled { get; set; } = false;
        private bool[] primes; // array used to determine primes

        public FindPrimesForm()
        {
            InitializeComponent();
            progressBar.Minimum = 2; // 2 is the smallest prime number
            percentageLabel.Text = $"{0:P0}"; // display 0 %
        }

        // handles getPrimesButton's click event
        private async void getPrimesButton_Click(object sender, EventArgs e)
        {
            // get user input
            var maximum = int.Parse(maxValueTextBox.Text);
```
```

**Fig. 21.6** | Displaying an asynchronous task’s progress and intermediate results. (Part I of 3.)