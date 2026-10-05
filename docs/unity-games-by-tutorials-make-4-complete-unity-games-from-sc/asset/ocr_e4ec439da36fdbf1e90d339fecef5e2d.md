# Unity Games by Tutorials

# Chapter 14: Saving Data

![](bbox=[0.229, 0.09, 0.77, 0.22])

Your first step is to create a new class that will hold two different values in public fields.

You'll use a DateTime type field to store the date and the best time run happened, and a Decimal type field to store the actual runtime level in seconds.

In the Project view, open the Scripts folder and right-click in the empty space. Choose the option to create a new C# script and name it PlayerTimeEntry. Open it for editing.

Replace the contents of the default Unity MonoBehaviour script for PlayerTimeEntry.cs with the following:

```
using System;

[Serializable]
public class PlayerTimeEntry
{
    public DateTime entryDate;
    public decimal time;
}
```

At the top of the class, you'll notice the Serializable marker, which allows the binary formatter to serialize and deserialize — a.k.a. pack to pack and unpack — this data class.

Save your work.

> Note: By the way, this script is different from your usual MonoBehaviour script — it won't inherit from MonoBehaviour. You'll use this class with the binary serialization system, and as such, it'll only be used to store data. It doesn't need to know or hold anything else except for the two values that'll be used to store a time entry.

Next, you'll be extending the GameManager.cs singleton script to handle saving and loading level runtime entries.

Open the GameManager.cs script for editing. Add the following new using statements to the top:

```
using UnityEngine.UI;
```