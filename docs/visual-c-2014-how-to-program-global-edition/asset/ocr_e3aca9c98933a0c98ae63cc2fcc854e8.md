# Chapter 23 Asynchronous Programming with ASYNC and await

```
// Fig. 23.4: FlickViewerForm.cs
// Invoking a web service asynchronously with class HttpClient
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Xml.Linq;

namespace Flickr
{
    public partial class FlickrForm : Form
    {
        // Use the Flickr API key here--you can get one at:
        // https://www.flickr.com/services/apps/create/apply
        private const string KEY = "YOUR API KEY HERE";

        // object used to invoke Flickr web service
        private static HttpClient FlickrClient = new HttpClient();

        Task<string> flickrTask = null; // Task<string> that queries Flick
        public FlickrForm()
        {
            InitializeComponent();
        }

        // initiate asynchronous Flickr search query;
        // display results when query completes
        private async void searchButton_Click(object sender, EventArgs e)
        {
            // if flickrTask. already running, prompt completion
            if (flickrTask?.Status != TaskStatus.RanToCompletion)
            {
                var result = MessageBox.Show(
                    "Cancel the current Flickr search",
                    "Are you sure?", MessageBoxButtons.YesNo,
                    MessageBoxIcon.Question);

                // determine whether user wants to cancel prior search
                if (result == DialogResult.No)
                {
                    return;
                }
                else
                {
                    flickrClient.CancelPendingRequests(); // cancel search
                }
            }
        }
    }
```

**Fig. 23.4** Invoking a web service asynchronously with class HttpClient. (Part I of 3) [Photos used in this example©Paul Deitel. All rights reserved.]