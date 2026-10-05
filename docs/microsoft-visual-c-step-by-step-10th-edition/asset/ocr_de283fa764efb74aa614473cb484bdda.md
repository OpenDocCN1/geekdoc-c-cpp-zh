```
private void Cancel()
{
    this.customers.Remove(this.Current);
    this.OnPropertyChanged(nameof(Current));
    this.IsBrowsing = true;
    this.LastError = String.Empty;
}
```