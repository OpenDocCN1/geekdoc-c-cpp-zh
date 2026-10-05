The examples so far have shown classes that implicitly implement an interface. If you revisit the ILandBound interface and the Horse class (shown next), you'll see that although the Horse class implements the ILandBound interface, nothing in the implementation of the NumberOfLegs method in the Horse class says that it is part of the ILandBound interface:

Click here to view code image

```
interface ILandBound
{
    int NumberOfLegs();
}

class Horse : ILandBound
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

This might not be an issue in a simple situation, but suppose the Horse class implemented multiple interfaces. There's nothing to prevent multiple interfaces from specifying a method with the same name, although they might have different semantics. For example, suppose you want to implement a transportation system based on horse-drawn coaches. A lengthy journey might be broken down into several stages, or legs. If you want to keep track of how many legs each horse pulled the coach, for you might define the following interface:

```
interface IJourney
{
    int NumberOfLegs();
}
```

Now, if you implement this interface in the Horse class, you have an interesting problem:

Click here to view code image

```
class Horse : ILandBound, IJourney
{
    ...
    public int NumberOfLegs()
    {
```