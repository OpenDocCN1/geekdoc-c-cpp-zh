```
int IComparable<Employee>.CompareTo(Employee other)
{
    if (other is null)
    {
        return 1;
    }
    if (this.Id > other.Id)
    {
        return 1;
    }
    if (this.Id < other.Id)
    {
        return -1;
    }
    return 0;
}
```