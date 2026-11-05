```
{
    try
    {
        int steelVolume = 4;
        int cutFactor = 2;
        ERPWarehouseIntegration oWhi = new ERPWarehouseIntegration();
        oWhi.CutSteelNoScrap(steelVolume, cutFactor);

        Console.Write("Steel fully consumed by cutting process");
        Console.ReadLine();
    }
    catch (Exception ex)
    {
        Console.Write(ex.Message);
        Console.ReadLine();
    }
}
```

*Code Listing 20: Modified Calling Code*

The console application now returns a perfect cut for the given factor and steel volume.

![](bbox=[0.3, 0.62, 0.82, 0.76])

*Figure 22: Contract.OldValue<> Passes*

While the preceding code listing is an extremely simple way to illustrate the use of the Contract.OldValue<> method, it can be expanded to provide much more benefit in validating that methods conform to certain business rules.

# Contract.Result<>

It is prudent to note that the Contract.Result<> method cannot be used in a method that has a void return type. To illustrate the use of this contract, we can reuse the previous code listings and modify them slightly.

```
public int ProductionVolumePerBin(int binVolume, int factor)
{
    Contract.Ensures(Contract.Result<int>() == binVolume,
        "The factor used will result in scrap. Please modify the cutting factor.");
}
```