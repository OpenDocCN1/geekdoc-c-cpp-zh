```
StreamReader r = new StreamReader(fs);
r.BaseStream.Seek(0, SeekOrigin.Begin);
TextBox1.Text = "";
while (r.Peek() > -1)
{
    TextBox1.Text += r.ReadLine() +
    System.Environment.NewLine;
}
r.Close();
bAF = true;
}
catch (SecurityException ex)
{
    bAF = false;
}
try
{
    FileAccessLib.Class1 FA = new
    FileAccessLib.Class1();
    string FileText = null;
    bLF = FA.AccessFile(ref FileText);
    TextBox2.Text = FileText;
}
catch
{
    bLF = false;
}
StatusBar1.Text = ((bAF & bLF) ? "Both app and the lib were allowed access." : ((bAF | bLF) ? ((bAF & ! bLF) ? "App was but lib was not allowed access." : "App wasn't but lib was allowed access") : "Neither app nor lib was allowed access."));
}
```

In Listing 36.29, a file on local hard disk is opened, changed, and then saved by class library (FileAccessLib) as well as by the application. The results for the class library and the application appear in the two text boxes.

+   7. Press the F5 key to execute the FileAccessApp application.

+   8. Click the Write and read file button. The output appears as shown in Figure 36.39.

![](bbox=[0.265, 0.6, 0.65, 0.875])

# Figure 36.39: Application running from local system

As you can see in Figure 36.39, the application as well as the class library can access the local file successfully.