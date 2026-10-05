```
if ((bool)addition.IsChecked)
{
    addValues();
}
else if ((bool)remainder.IsChecked)
{
    remainderValues();
}
else
{
    throw new InvalidOperationException("No operator selected");
}
```