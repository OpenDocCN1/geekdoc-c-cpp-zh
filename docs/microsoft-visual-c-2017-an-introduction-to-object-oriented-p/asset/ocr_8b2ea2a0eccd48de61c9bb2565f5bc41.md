the shaded statement, the subscript is erroneously set to 2 instead of 1 for the higher tax rate. If this subscript is used with the taxRate array in the next statement, it will be out of bounds.

```
class Tax {
    private static static double[] taxRate = {0.06, 0.07};
    private static double CUTOFF = 20.00;
    public static double DetermineRate(double price)
{
        int subscript;
        double rate;
        if(price <= CUTOFF)
            subscript = 0;
        else
            subscript = 2;
        rate = taxRate[subscript];
        return rate;
    }
}
```

Figure 11-27 The Tax class

Assume that your company has also created a revised PriceList class, as shown in Figure 11-28. This class is similar to the one in Figure 11-22, except it includes a tax calculation and calls the DetermineTaxRate() method in the shaded statement.

```
class PriceList {
    private static double[] price = {15.99, 27.88, 34.56, 45.89};
    public static void DisplayPrice(int item)
{
        double tax;
        double total;
        double pr;
        pr = price[item];
        tax = pr * Tax.DetermineTaxRate(pr);
        total = pr + tax;
        WriteLine("The total price is " + total.ToString("C")");
    }
}
```

Figure 11-28 The PriceList class that includes a call to the Tax class method