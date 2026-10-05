# Chapter 10 / Trees 263

```
Xmid = (Area.Left + Area.Right) / 2
Ymid = (Area.Top + Area.Bottom) / 2
End Constructor
QuadtreeNode
```

The valueMaxSize indicates the maximum number of items a node can hold before it is split into quadrants.
The Items property contains the items that the node holds. If the node is internal, it is null, and the items are stored in the node's child subtrees.
The Area property holds the rectangle that the node represents in two-dimensional space.
The Xmid and Ymid values give the middle X and Y coordinates of the Area rectangle. These are used to determine which quadrant contains an item.
This class provides a constructor that initializes the node's Area and initializes the Xmid and Ymid properties. You could calculate Xmid and Ymid whenever you need them, but those values are used frequently (at least for leaf nodes), so you can save time by initializing them.
The following pseudocode shows how a quadtreeNode can add a new item to its subtree:

```
// Add item to this node's subtree.
AddItem(Item: newItem)
// See if this quadtree node is full.
If ((Items != null) && (Items.Count + 1 > MaxItems)) Then
    // divide quad node.
    float w = (Area.Right - Area.Left) / 2
    float h = (Area.Bottom - Area.Top) / 2
    NWChild = New QuadtreeNode(
        Rectangle(Area.Left, Area.Top, w, h))
    NEChild = New QuadtreeNode(
        Rectangle(Area.Left + w, Area.Top, w, h))
    SEChild = New QuadtreeNode(
        Rectangle(Area.Left + w, Area.Top + h, w, h))
    SWChild = New QuadtreeNode(
        Rectangle(Area.Left, Area.Top + h, w, h))

// Move the points into the appropriate subtrees.
For each Item in Items
    If (Item.Y < Ymid) Then
        If (Item.X < Xmid) NWChild.AddItem(Item)
        Else NEChild.AddItem(Item)
    Else
        If (Item.X < Xmid) SWChild.AddItem(Item)
        Else SEChild.AddItem(Item)
    End If
Next item

// Remove this node's Items list.
```