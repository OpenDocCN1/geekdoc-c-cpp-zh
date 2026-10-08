# LISTING 16-15 (continued)

```
// Set up Ajax event handling
Chart1.Click += new ImageMapEventHandler(Chart1.Click);
foreach (Series series in this.Chart1.Series)
{
    series.PostBackValue = "Series: " + series.Name + "
```

```
protected void Chart1_Click(object sender, ImageEventArgs e)
{
Chart1.Titles["MessageTitle"].Text = "Nothing";
string[] input = e.PostBackValue.Split(',\');
if (input.Length == 2)
{
    string[] seriesData = input[0].Split(',\');
    if (input[0].Equals("Chart"))
{
Chart1.Titles["MessageTitle"].Text = "Last Clicked Element: " + 
        seriesData[0] + " #" + seriesData[1];
    }
else if (input[0].Equals("Chart"))
{
    var hit = this.Chart1.HitTest(
Int32.Parse(seriesData[0]),
Int32.Parse(seriesData[1]));
    if (hit == null)
{
Chart1.Titles["MessageTitle"].Text = 
        "Last Clicked Element: " + hit.ChartElementType.ToString();
    }
}\}
}
```