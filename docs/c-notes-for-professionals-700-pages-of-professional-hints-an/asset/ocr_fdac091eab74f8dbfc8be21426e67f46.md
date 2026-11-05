# Chapter 116: BackgroundWorker

# Section 116.1: Using a BackgroundWorker to complete a task

The following example demonstrates the use of a BackgroundWorker to update a WinForms ProgressBar. The backgroundWorker will update the value of the progress bar without blocking the UI thread, thus showing a reactive UI while work is done in the background.

```
```csharp
namespace BgWorkerExample
{
    public partial class Form1 : Form
    {
        //a new instance of a backgroundWorker is created.
        BackgroundWorker bgWorker = new BackgroundWorker();

        public Form1()
        {
            InitializeComponent();

            prgProgressBar.Step = 1;

            //this assigns event handlers for the backgroundWorker
            bgWorker.DoWork += bgWorker_DoWork;
            bgWorker.RunWorkerCompleted += bgWorker_WorkComplete;

            //tell the backgroundWorker to raise the "DoWork" event, thus starting it.
            //Check to make sure the background worker is not already running.
            if(!bgWorker.IsBusy)
                bgWorker.RunWorkerAsync();
        }

        private void bgWorker_DoWork(object sender, DoWorkEventArgs e)
        {
            //this is the method that the backgroundworker will perform on in the background thread.
            /* One thing to note! A try catch is not necessary as any exceptions will terminate the
            backgroundWorker and report
            the error to the "RunWorkerCompleted" event */
            CountToY();
        }

        private void bgWorker_WorkComplete(object sender, RunWorkerCompletedEventArgs e)
        {
            //e.Error will contain any exceptions caught by the backgroundWorker
            if (e.Error != null)
            {
                MessageBox.Show(e.Error.Message);
            }
            else
            {
                MessageBox.Show("Task Complete!");
                prgProgressBar.Value = 0;
            }
        }

        // example method to perform a "long" running task.
        private void CountToY()
        {
            int x = 0;
```
```