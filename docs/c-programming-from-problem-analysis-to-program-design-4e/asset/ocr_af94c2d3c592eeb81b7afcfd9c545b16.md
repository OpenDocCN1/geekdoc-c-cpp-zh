ComputeAverageForMonth ( ) method adds additional functionality to the Manatee class. It returns the average for a given month.

Figure 7-14 shows the Structured English, or pseudocode, used to design the step-by-step processes for the behaviors of the methods of the ManateeApp example.

```
CalculateAvg()
set totalCount = 0
loop while (more manateeCounts)
{
    totalCount = totalCount + manateeCount
}
avg = (double)totalCount / manateeCount.Length

GetIndexOfMostSightings()
maxCntIndex = 0
index = 1
loop while (more manateeCounts)
{
    if (manateeCount[index] > manateeCount[maxCntIndex])
        maxCntIndex = index
    index++
}
return maxCntIndex

ComputeAverageForMonth(string mon) : monAverage
total = 0
days = 0
index = 0
loop while (more sightings)
{
    if (sightDate[index].StartsWith(mon))
    {
        total += manateeCount[index]
        days++
    }
}
if (days > 0)
    monAverage = (double) total / days
else
    monAverage = 0
return monAverage

ReturnMonth(string someDate) : monthName
define monthNameArray
tempArray = someDate.Split('/')
tempArray = tempArray.Trim(0)
intMonth = Convert.ToInt(tempArray)
monthName = MonthNameArray[intMonth]
return monthName
```

# FIGURE 7-14 ManateeSighting class methods behavior

After the algorithm is developed, the design should be checked for correctness. You might develop a table now with test values using a standard calculator. Desk check the pseudocode to ensure you are getting the results expected. After your program is running, you can validate the correctness by comparing results you produce with your program against values you produced with the calculator during your design walk-through.