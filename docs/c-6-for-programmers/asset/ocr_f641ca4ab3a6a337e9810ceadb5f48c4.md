```
// change LinkColor after it has been clicked
cDriveLinkLabel.LinkVisited = true;

System.Diagnostics.Process.Start(@"C:\");
}

// load www.deitel.com in web browser
private void deitelLinkLabel_LinkClicked(object sender,
LinkLabelLinkClickedEventArgs e)
{
    // change LinkColor after it has been clicked
    deitelLinkLabel.LinkVisited = true;

    System.Diagnostics.Process.Start("http://www.deitel.com");
}

// run app Notepad
private void notepadLinkLabel_LinkClicked(object sender,
LinkLabelLinkClickedEventArgs e)
{
    // change LinkColor after it has been clicked
    notepadLinkLabel.LinkVisited = true;

    // program called as if in run
    // menu and full path not needed
    System.Diagnostics.Process.Start("notepad");
}
}
```

Click first LinkLabel to look at contents of C: drive

![](bbox=[0.22, 0.62, 0.38, 0.75])

![](bbox=[0.48, 0.58, 0.85, 0.75])

Click second LinkLabel to go to Deitel website

![](bbox=[0.22, 0.82, 0.38, 0.92])

![](bbox=[0.48, 0.78, 0.85, 0.92])