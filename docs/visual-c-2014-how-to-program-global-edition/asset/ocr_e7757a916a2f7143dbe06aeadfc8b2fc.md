# 12.7 Case Study: Creating and Using Interfaces 537

```
// property that gets and sets the quantity on the invoice
public int Quantity
{
    get
    {
        return quantity;
    }
    set
    {
        if (value < 0) // validation
            throw new ArgumentOutOfRangeException(nameof(value),
                $"{nameof(Quantity)} must be >= 0");
        quantity = value;
    }
}
// property that gets and sets the price per item
public decimal PriceItem
{
    get
    {
        return priceItem;
    }
    set
    {
        if (value < 0) // validation
            throw new ArgumentOutOfRangeException(nameof(value),
                $"{nameof(PriceItem)} must be >= 0");
        priceItem = value;
    }
}
// string representation of Invoice ToString() =>
public override string ToString() =>
    $"{number: {PartDescription}}\n" +
    $"{quantity: {Quantity}\n per item: {PriceItem:C}";
// method required to carry out contract with interface IPayable
public decimal GetPaymentAmount() => Quantity * PriceItem;
```

Fig. 12.12 | Invoice class implements IPayable (Part 2 of 2)

Line 5 indicates that Invoice class implements interface IPayable. Like all classes, class Invoice also implicitly inherits from class object. All objects of a class can implement multiple interfaces, in which case they have the is-a relationship with each implemented interface type.