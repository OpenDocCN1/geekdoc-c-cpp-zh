```
```csharp
aMinute = aMinute % 60;
// grab seconds
aSecond = (int)currentTime % 60;

// grab milliseconds
aMillis = (int)(currentTime * 100) % 100;
```
```

After minutes, seconds, and milliseconds values have been calculated and stored in the integer variables aMinute, aSecond, and aMillis, three new strings called seconds, minutes and mills are built from them:

```
```csharp
// format strings for individual mm/ss/mills
tmp = (int)aSecond;
seconds = tmp.ToString("D2"); // ToString()
```
```

formats ... in this case, D followed by how many numbers

```
```csharp
tmp = (int)aMinute;
minutes = tmp.ToString("D2");

tmp = (int)aHour;
hour = tmp.ToString("D2");

tmp = (int)aMillis;
mills = tmp.ToString("D2");
```
```

```
```csharp
// pull together a formatted string to return
timeString = minutes + ":" + seconds + ":" +
mills;
```
```

In C#, you can convert numbers to strings with the ToString() function.
Something great about ToString() is that you can also pass in a format string. The
format string takes the form of a letter followed by an integer number. Above, we
use the format string D2 to tell ToString() to use two digits, which will convert
our times into a neat format ready to display. Note that you can set as many digits
as you like, simply by changing the number in the format string. For more infor-
mation on format strings, you can find a full breakdown and a full list of all of the
available formatting options online at Microsoft's .NET Standard numeric for-
mat strings page: https://docs.microsoft.com/en-us/dotnet/standard/base-types/
standard-numeric-format-strings

Once the individual parts of the formatted time string are ready, we put them
all together into a final timeString and return it at the end of the function, like this:

```
```csharp
// pull together a formatted string to return
timeString=minutes+":"+seconds+":"+mills;

return timeString;
}
```
```

At the very end of the script, a GetTime() function provides a way for other
scripts to process the value of currentTime:

```
```csharp
public int GetTime ()
{
    // remember to call UpdateTimer() before trying to
use this function, otherwise the time value will
    // not be up to date
    return (int)currentTime;
}
```
```