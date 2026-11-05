```
```
int QtyAvailable = MaxBinQuantity - CurrentBinQuantity;
return QtyAvailable;
}
```
```

*Code Listing 10: Assert Static Check*

The code in Code Listing 10 checks to see if the Bin containing the parts has enough space to contain the required quantity. With the Assert method, we are letting the static checker inspect the value of the QuantityRequired variable. If we had to pass through a value of 77 for QuantityRequired, we would see the static checker emit a warning and fail the build (remember, we turned on Fail build on warnings in the Code Contracts property page).

![](bbox=[0.12, 0.32, 0.88, 0.5])

*Figure 13: Assert Failed*

If we had to modify the code in Code Listing 10 to contain an Assume, the output would be quite different indeed. Consider the code in the following listing.

```
```
public void CompleteBinPreparation(int quantityRequired)
{
    QuantityRequired = quantityRequired;
    int available = BinQtyAvailable();
    Contract.Assume(QuantityRequired <= available, "Quantity required exceeds available bin quantity");
}

public int BinQtyAvailable()
{
    MaxBinQuantity = 75;
    CurrentBinQuantity = 50;
    int QtyAvailable = MaxBinQuantity - CurrentBinQuantity;
    return QtyAvailable;
}
```
```

*Code Listing 11: Assume Static Check*