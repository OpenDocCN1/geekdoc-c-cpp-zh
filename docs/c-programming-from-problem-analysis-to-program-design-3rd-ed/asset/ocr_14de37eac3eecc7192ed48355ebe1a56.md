```
```csharp
set
{
    lname = value;
}
}

public string ID
{
    get
    {
        return id;
    }
    set
    {
        id = value;
    }
}

public void FillPointsScoredArray(int [ ] s)
{
    pointsScored = new int [numberOfGames];
    for (int i = 0; i < pointsScored.Length; i++)
        pointsScored[i] = s[i];
}

public void ComputeAverage( )
{
    double total = 0;

    foreach(int s in pointsScored)
        total += s;
    if(pointsScored.Length > 0)
        avg = total / pointsScored.Length;
}
}
}
/* PlayerApp.cs    Author: Doyle
 * Application that instantiates
 * Player class. Creates an array
 * of player objects that can be
 * used to display individual
 * records or do stats
 * on the entire team.
 */
```
```