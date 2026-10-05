```
return 4;
}
```

This is legal code, but does the horse have four legs or has it pulled the coach for four legs of the journey? The answer as far as C# is concerned is both! By default, C# does not distinguish which interface the method is implementing, so the same method actually implements both interfaces.

To solve this problem and disambiguate which method is part of which interface implementation, you can implement interfaces explicitly. To do this, you specify which interface method belongs to when you implement it, like this:

Click here to view code image

```
class Horse : ILandBound, IJourney
{
  ..
  int ILandBound.NumberOfLegs()
  {
    return 4;
  }
  int IJourney.NumberOfLegs()
  {
    return 3;
  }
}
```

Now you can see that the horse has four legs and has pulled the coach for three legs of the journey.

Apart from prefixing the name of the method with the interface name, there’s one other subtle difference in this syntax: the methods are not marked public. You cannot specify the protection for methods that are part of an explicit interface implementation. This leads to another interesting phenomenon. If you create a Horse variable in the code, you cannot actually invoke either of the NumberOfLegs methods because they are not visible. As far as the Horse class is concerned, they are both private. In fact, this makes sense. If the methods were visible through the Horse class, which would make the following code actually invoke, the one for the ILandBound interface or the one for the IJourney interface?

Click here to view code image