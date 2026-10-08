# Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

```
blueToolStripMenuItem.Checked = true;
}
n// update Menu state and color display red
private void redToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // reset checkmarks for Color ToolStripMenuItems
    ClearColor();

    // set color to Red
    displayLabel.ForeColor = Color.Red;
    redToolStripMenuItem.Checked = true;
}

// update Menu state and color display green
private void greenToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // reset checkmarks for Color ToolStripMenuItems
    ClearColor();

    // set color to Green
    displayLabel.ForeColor = Color.Green;
    greenToolStripMenuItem.Checked = false;
}

// reset checkmarks for Font ToolStripMenuItems
private void ClearFont()
{
    // clear all checkmarks
    timesToolStripMenuItem.Checked = false;
    courierToolStripMenuItem.Checked = false;
    comicToolStripMenuItem.Checked = false;
}

// update Menu state and set Font to Times New Roman
private void timesToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    // reset checkmarks for Font ToolStripMenuItems
    ClearFont();

    // set Times New Roman font
    timesToolStripMenuItem.Checked = true;
    displayLabel.Font = new Font("Times New Roman", 14,
    displayLabel.Font.Style);
```

**Fig. 15.7** | Using menus to change font colors and styles. (Part 3 of 5 )