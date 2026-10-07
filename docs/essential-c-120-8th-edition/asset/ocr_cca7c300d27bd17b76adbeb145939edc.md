```
public static void BubbleSort(int[] items)
{
    int i;
    int j;
    int temp;

    if(items == null)
    {
        return;
    }

    for(i = items.Length - 1; i >= 0; i--)
    {
        for(j = 1; j <= i; j++)
        {
            if(items[j] > items[j - 1])
            {
                temp = items[j - 1];
                items[j - 1] = items[j];
                items[j] = temp;
            }
        }
    }
    // ...
}
```

This method will sort an array of integers in ascending order.
Suppose you need to sort the integers in Listing 13.1 in either ascending or descending order. You could duplicate the code and replace the greater-than operator with a less-than operator, but it seems like a bad idea to replicate several lines of code merely to change a single operator. As a less verbose alternative, you could pass in an additional parameter indicating how to perform the sort, as shown in Listing 13.2.

# LISTING 13.2: BubbleSort() Method, Ascending or Descending

```
public class SimpleSort2
{
    public enum SortType
    {
        Ascending,
        Descending
    }
}
```