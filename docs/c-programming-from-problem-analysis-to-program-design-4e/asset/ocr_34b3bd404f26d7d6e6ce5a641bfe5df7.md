# EXAMPLE 4.8

```
public double NoOfSqYards
{
    get
    {
        return noOfSqYards;
    }
    set
    {
        noOfSqYards = value;
    }
}
public double Price
{
    get
    {
        return pricePerSqYard;
    }
    set
    {
        pricePerSqYard = value;
    }
}
```

A standard naming convention in C# for properties is to use the same name as the instance variable or field. The exception is that the property identifier starts with an uppercase character. NoOfSqYards follows that convention. To call attention to the fact that the names do not have to match, Price in Example 4-8 did not follow that convention. If the property naming convention is followed, the property name associated with the PricePerSqYard data member would be PricePerSqYard. This is illustrated in Example 4-9.

# EXAMPLE 4.9

```
public double PricePerSqYard
{
    get
    {
        return pricePerSqYard;
    }
    set
    {
        pricePerSqYard = value;
    }
}
```

Using the same name, as shown in Example 4-9 enables the data member to be quickly associated with the property member.