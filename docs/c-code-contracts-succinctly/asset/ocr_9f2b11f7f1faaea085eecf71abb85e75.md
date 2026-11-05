With the current version 1.9.10714.2 of Code Contracts, the build errors not being output to the Error List has been identified as a bug in the release for Visual Studio 2015. This bug has been fixed and will be included in the next release of Code Contracts. For more information on this issue relating to Code Contracts for Visual Studio 2015, have a look at pull request 166 and issue 137 on GitHub. If you want to view all the open issues regarding Code Contracts, have a look at the Issues on the Code Contracts GitHub page.

Code Contracts is the result of a handful of dedicated individuals who continually work to improve the current version. It's up to users like us to report issues we come across, and in doing so, build a healthy community of influencers and a more stable product. Lastly, since it's open source, you can contribute to Code Contracts and be a part of this incredible Visual Studio extension.

# The Code Contract postcondition

The Code Contract postcondition is the method under contract's way of guaranteeing to the calling code that it will return a specific result if all the preconditions are met. Let us go back to the analogy of a bank and a loan for which a contract is drawn up. The bank ensures that the loan will have a fixed interest rate, but only if the repayments are made on time and for the amount due. The payments made by you can be equated to the preconditions of the Code Contract. The fact that the bank ensures a fixed interest rate can be equated to the postcondition.

It is therefore no surprise that the syntax of Code Contract postconditions use the Ensures method. Another interesting point to take note of is that while the postcondition validates the result of the method under contract, it must appear immediately after the preconditions in the method. Consider the following code sample:

```
```csharp
public static Warehouse AddSerializedItem(string productCode, int serialNumber, int qty)
{
    Contract.Requires<SerialNumberException>
        (serialNumber >= 10000001, "Invalid Serial number");
    Contract.Ensures(Contract.Result<Warehouse>() != null);

    ProductCode = productCode;
    SerialNumber = serialNumber;
    Quantity = qty;

    return CreateItem();
}
```
```

Code Listing 4: Contract Postcondition

As you can see from the previous code listing, I have expanded our method slightly. I have added the postcondition that tells the calling code that the return value of this method will be of type Warehouse and that it will not be null. The calling code therefore does not need to check if