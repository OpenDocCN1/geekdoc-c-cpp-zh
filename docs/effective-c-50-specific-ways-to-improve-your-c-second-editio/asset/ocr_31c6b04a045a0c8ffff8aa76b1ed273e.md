```
if (value is PayrollData)
    data.Add((PayrollData)value);
return data.Count;
}

public void Clear() { data.Clear(); }

public bool Contains(object value)
{
    if (value is PayrollData)
        return data.Contains((PayrollData)value);
    else
        // If the argument isn't the right type,
        // it must not be here.
        return false;
}

public int IndexOf(object value)
{
    if (value is PayrollData)
        return data.IndexOf((PayrollData)value);
    else
        return -1;
}

public void Insert(int index, object value)
{ if (value is PayrollData)
    data.Insert(index, (PayrollData)value); }

public bool IsFixedSize
{ get { return (data as IBindingList).IsFixedSize; } }

public bool IsReadOnly
{ get { return (data as IBindingList).IsReadOnly; } }

public void Remove(object value)
{
    if (value is PayrollData)
        data.Remove((PayrollData)value);
}
```