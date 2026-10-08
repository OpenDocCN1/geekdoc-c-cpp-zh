# 476 Using the System.DrawingNamespace

```
else {
    ScoreCheck.SetError(score, **);
    //Add the score written to the points
    points.Text = (int)points.Text + (int)scoreBox.Text;
}
catch (System.InvalidCastException) {
    //Something other than a number
    if (scoreBox.Text.Length > 0) {
        ScoreCheck.SetError(score, "Score must be a number");
    }
}
c catch (Exception ex) {
    //Ek!
    MessageBox.Show("Something went wrong! " * + ex.Message);
}
//Check the score
if ((int)points.Text / (int)otherPlayer.Text > 1.5) {
    WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6)
    + " Skunked em!!";
} else {
    WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6)
    + " Won!!";
}
WinMessage.Visible = true;
```

All this changing screen values causes the Paint event of the form to fire — every time C# needs to change the look of a form for any reason, this events — so I just drew a little code in that event handler that would draw my board for me:

From that point, my largest concern is drawing the board itself.

# Drawing the board

I need to paint a right on a form to create the image of the board for my cribbage application, so use the CreateGraphics method of the form control. From there, I need to complete these tasks:

+   - Paint the board brown using a brush.
- Draw rows of little circles using a pen.
- Fill in the hole if that is the right score.
- Clean up my supplies.