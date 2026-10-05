```
public class Tree<TItem> where TItem : IComparable<TItem>
{
    public TItem NodeData { get; set; }
    public Tree<TItem>? LeftTree { get; set; }
    public Tree<TItem>? RightTree { get; set; }
}
```