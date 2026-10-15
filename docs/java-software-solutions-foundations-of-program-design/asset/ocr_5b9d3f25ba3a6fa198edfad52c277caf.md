# LISTING 13.2 continued

```
```java
{
    String result = "";
    MagazineNode current = list;
    while (current != null)
    {
        result += current.magazine + "\n";
        current = current.next;
    }
    return result;
}

// An inner class that represents a node in the magazine list.
// The public variables are accessed by the MagazineList class.
private class MagazineNode
{
    public Magazine magazine;
    public MagazineNode next;

    // Sets up the node
    public MagazineNode (Magazine mag)
    {
        magazine = mag;
        next = null;
    }
}
```
```