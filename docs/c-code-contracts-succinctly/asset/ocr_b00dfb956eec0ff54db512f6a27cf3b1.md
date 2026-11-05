# Contract.OldValue<>

A couple of years ago, I worked on a project for a steel manufacturer. They had a very specific scrap process to follow when off-cuts were produced by cutting steel plates into specific sizes. Another project I worked on had a specific scrap workflow to process. Scrap is something many companies take very seriously, and they need to manage the process carefully.

For the next example of Code Contracts, I will use the scrap process to illustrate the use of the Contract.OldValue<> method. I have to mention, though, that the Contract.OldValue<> method can only be used in the conditional expression for the Ensures contract.

Let us assume that the steel manufacturer needs to minimize the amount of off-cuts produced by the cutting process. To do this, they use a calculation that takes the volume of steel to be cut, and calculate the amount of steel that can be used based on the cutting factor. A perfect cut means that if the volume of steel is 10 m³, then the resulting cut of steel will also be equal to 10 m³. All of the steel has therefore been consumed and resulted in zero off-cuts.

An imperfect cut would result in less than the original volume of steel, and this would mean that the user will need to change the cutting factor until they can ensure a near-perfect cut. Without going into more detailed specifics regarding thresholds and limits, let us assume that if anything other than a perfect cut is returned, the cutting process is not approved.

Consider the following code listing.

```
public void CutSteelNoScrap(int volumeSteel, int factor)
{
    Contract.Ensures(volumeSteel != 0, "The volume of steel can't be zero");
    Contract.Ensures(Contract.OldValue<int>(volumeSteel)
        == CutSteel(volumeSteel, factor) + volumeSteel,
        "The factor used will result in scrap. Please modify the cutting factor.");
    // Process steel to cut
}

private int CutSteel(int volumeToCut, int factor)
{
    return volumeToCut % factor;
}
```

*Code Listing 18: Contract.OldValue<> Implementation*

As you can see, I have simply used a modulus operator to simulate the existence of off-cuts based on the incorrect factor. The modulus operator simply returns the remainder of a division and is denoted by the % operator. Therefore, the following is true:

19 % 5 = 4

12 % 4 = 0