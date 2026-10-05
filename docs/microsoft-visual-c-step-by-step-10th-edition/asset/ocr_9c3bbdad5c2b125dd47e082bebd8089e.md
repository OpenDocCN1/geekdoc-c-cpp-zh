```
using System;
using System.Collections.Generic;
using System.Collections;
class BasicCollection<T> : IEnumerable<T>
{
    private List<T> data = new List<T>();
    public void FillList(params T [] items)
    {
        foreach (var datum in items)
        {
            data.Add(datum);
        }
    }

IEnumerator<T> IEnumerable<T>.GetEnumerator()
{
    foreach (var datum in data)
    {
        yield return datum;
    }
}
IEnumerator IEnumerable.GetEnumerator()
{
    // Not implemented in this example
    throw new NotImplementedException();
}
```

The GetEnumerator method appears to be straightforward, but it warrants closer examination. The first thing to note is that it doesn't appear to return an Enumerator<T> type. Instead, it loops through the items in the data array, returning each item in turn. The key is the use of the yield keyword. This keyword indicates the value that should be returned by each iteration. If it helps, you can think of the yield statement as calling a temporary halt to the method, passing back a value to the caller. When the caller needs the next value, the GetEnumerator method continues at the point at which it left off, looping around and then yielding the next value. Eventually, the data is exhausted, the loop finishes, and the GetEnumerator method terminates. At this point, the iteration is complete.