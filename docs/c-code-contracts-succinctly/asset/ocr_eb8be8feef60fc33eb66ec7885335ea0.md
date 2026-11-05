![](bbox=[0.12, 0.11, 0.9, 0.27])

Figure 54: All IntelliTest Tests Passed

From the test result we can see that the ProductionVolumePerBin() method has held up to the requirements imposed by our Code Contracts. It has also generated six warnings, which I'll discuss shortly.

The calling code can now implement the ProductionVolumePerBin() method without needing to cater for invalid values being returned. It knows that the method will return a perfect cut every time. The only check that needs to be done is to see whether a new factor has been suggested or if the supplied factor is valid.

```
int binVol = 20;
int factor = 3;
CodeContractsDemoProject.ERPWarehouseIntegration owhi =
    new CodeContractsDemoProject.ERPWarehouseIntegration();
int result = owhi.ProductionVolumePerBin(binVol, factor);
if (owhi.CalculatedCuttingFactor != factor &&
    owhi.CalculatedCuttingFactor != 0)
{
    Console.Write($"The supplied cutting factor of {factor} resulted in "
        + "an imperfect cut. The system suggests using the following "
        + $"cutting factor: {owhi.CalculatedCuttingFactor}");
}
else
    Console.Write($"The cutting factor of {factor} resulted in 0 scrap");

Console.ReadLine();
```

Code Listing 67: Code Calling ProductionVolumePerBin

You will notice that I am using string interpolation in the Console.Write each time. This is one of the new features in C# 6. The preceding code only needs to check the CalculatedCuttingFactor property to see if the cutting factor has changed. It knows that under contract, the ProductionVolumePerBin() method will always result in a perfect cut.

We can further improve the preceding code, but the concept I wanted to illustrate is clear. Code Contracts lend themselves very well to tests created with IntelliTest in Visual Studio Enterprise 2015. You can combine the power of both technologies to create highly robust code and highly enforced business rules to make your applications perform well in a production environment.