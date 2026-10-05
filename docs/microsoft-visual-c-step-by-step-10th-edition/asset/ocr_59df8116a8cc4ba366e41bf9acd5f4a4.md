Click here to view code image

```
private void Next()
{
    if (this.customers.Count - 1 > this.currentCustomer)
    {
        this.currentCustomer++;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
        ...
    }
}
```

```
private void Previous()
{
    if (this.currentCustomer > 0)
    {
        this.currentCustomer--;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    }
}
```

```
private void First()
{
    this.currentCustomer = 0;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
}
```

```
private void Last()
{
    this.currentCustomer = this.customers.Count - 1;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    ...
}
```

+   5. Open the MainPage.xml file in the Design View window.

+   6. Add the ProgressRing control shown next to the top-level Grid control:

Click here to view code image

```
<Page
```