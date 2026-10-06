# CHAPTER 12 Using Controls

If you double-click a LinkLabel in the IDE, a method shell is created for you in the format xxx_LinkClicked(), where xxx is the Name of the property belonging to the LinkLabel. (This corresponds to what when you double-click a Button in the IDE). For example, double-clicking a linkLabel1_LinkClicked() method shell. As Button Click() methods, you usually want to rename LinkClicked() methods so they conventionally start with an uppercase letter. Figure 12-7 shows the two generated methods for the Form in Figure 12-7 when the automatically-created methods have been altered to start with uppercase

![](bbox=[0.137, 0.096, 0.417, 0.248])

Figure 12-6 A Form with two LinkLabels In Figure 12-7, the two shaded statements are the only parts of the code that were generated automatically. The programmer added these lines to indicate which actions should occur when a user clicks the corresponding LinkLabel in a running application.

```
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }
    private void LinkLabel1_LinkClicked(object sender,
        LinkLabelClickedEventArgs e)
    {
        System.Diagnostics.Process.Start("IExplore",
        "http://www.cengage.com");
    }
    private void LinkLabel2_LinkClicked(object sender,
        LinkLabelClickedEventArgs e)
    {
        System.Diagnostics.Process.Start(
        ("C:\CSharp\Chapter12\Policy.txt");
    }
}
```

Figure 12-7 Two LinkClicked() methods

If you using System.Diagnostics; at the top of your file, you can eliminate the references in Figure 12-7 and refer to the process simply as Process.Start.

When you view in the IDE, there will not be as many line breaks as you see in the code figures in this chapter. The line breaks have been inserted so the lines fit better on the pages of this book.