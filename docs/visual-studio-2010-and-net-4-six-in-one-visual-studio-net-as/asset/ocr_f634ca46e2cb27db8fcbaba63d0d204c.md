There another method called Filter where you can use a CompareMethod enumeration to define the operation for filtering. Be aware of the fact that the condition is defined for those data points that should be omitted from the result set. The following snippet demonstrates this:

```
private void FilterLessThanMenuItem_Click(object sender, EventArgs e)
    chart1.DataManipulator.FilterSetEmptyPoints = true;
    chart1.DataManipulator.Filter(CompareMethod.MoreThan, 50.0,
    "Series1", "Series2");
```

The intention is to display only those points in the result that have a Y value less than 50, so we must use the CompareMethod.MoreThan reflection to reverse this logic.

When you need more filtering logic (for example, criteria not supported by the Compare Method enumeration), you can create a data point filter and pass class to the Filter method. A data point filter must implement the IDataPointFilter interface, as the following code snippet shows:

```
private class BetweenFilter : IDataPointFilter
    private double lowerValue;
    private double upperValue;

    public BetweenFilter(double lower, double upper)
{
        lowerValue = lower;
        upperValue = upper;
    }
    bool IDataPointFilter.FilterDataPoint(DataPoint point, Series series, int pointIndex)
{
        return point.YValues[0] > upperValue || point.YValues[0] < lowerValue;
    }
```

The BetweenClass implements a data point filter that will put those data points into the result set that are within the specified range. The FilterDataPoint retrieves true if the data point should be omitted from the result set; otherwise, it is false. As you can see, the reverse condition is applied in this method — the condition defines the data point that should be omitted from the result set.

You can use the data point filter class as shown in the following code:

```
private void CustomFilterMenuItem_Click(object sender, EventArgs e)
{
    chart1.DataManipulator.FilterSetEmptyPoints = true;
    chart1.DataManipulator.Filter(new BetweenFilter(10.0, 60.0),
    "Series1", "Series2");
```