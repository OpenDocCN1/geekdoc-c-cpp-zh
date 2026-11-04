![](bbox=[0.03, 0.08, 0.75, 0.45])

FIGURE 6.5 A type hierarchy with an IsFresh virtual method.

All is good and well if you control the Food type and its descendants: Add the IsFresh virtual method, implement it for each type that needs specialized treatment, and just call the virtual method where required. The runtime will take care of making sure the right method is called for you.

But when you're dealing with an existing set of types you can't extend, how do you go ahead and implement a similar EnsureFreshness procedure? The answer lies in type checks: For each food item you're scanning, you'll check the type and take the appropriate action based on that outcome. A potential approach—which we refine in the next section—looks like this:

```
public void EnsureFreshness()
{
    foreach (Food item in stock)
    {
        if (!IsFresh(item))
        {
            store.TossOut(item);
        }
    }
}

private bool IsFresh(Food item)
{
    if (item is Fruit)
    {
```