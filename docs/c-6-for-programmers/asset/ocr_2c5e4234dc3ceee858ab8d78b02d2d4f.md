```
// update Menu state and set Font to Courier
private void courierToolStripMenuItem_Click(
    object sender, EventArgs e)
{
    // reset checkmarks for Font ToolStripMenuItems
    ClearFont();

    // set Courier font
    courierToolStripMenuItem.Checked = true;
    displayLabel.Font = new Font("Courier", 14,
        displayLabel.Font.Style);
}

// update Menu state and set Font to Comic Sans MS
private void comicToolStripMenuItem_Click(
    object sender, EventArgs e)
{
    // reset checkmarks for Font ToolStripMenuItems
    ClearFont();

    // set Comic Sans font
    comicToolStripMenuItem.Checked = true;
    displayLabel.Font = new Font("Comic Sans MS", 14,
        displayLabel.Font.Style);
}

// toggle checkmark and toggle bold style
private void boldToolStripMenuItem_Click(object sender, EventArgs e)
{
    // toggle checkmark
    boldToolStripMenuItem.Checked = !boldToolStripMenuItem.Checked;

    // use Xor to toggle bold, keep all other styles
    displayLabel.Font = new Font(displayLabel.Font,
        displayLabel.Font.Style ^ FontStyle.Bold);
}

// toggle checkmark and toggle italic style
private void italicToolStripMenuItem_Click(
    object sender, EventArgs e)
{
    // toggle checkmark
    italicToolStripMenuItem.Checked =
        !italicToolStripMenuItem.Checked;

    // use Xor to toggle italic, keep all other styles
    displayLabel.Font = new Font(displayLabel.Font,
        displayLabel.Font.Style ^ FontStyle.Italic);
}
```