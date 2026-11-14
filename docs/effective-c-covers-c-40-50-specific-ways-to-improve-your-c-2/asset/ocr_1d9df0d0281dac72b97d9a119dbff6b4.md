```
public void RemoveAt(int index)
{ data.RemoveAt(index); }
```

```
public object this[int index]
{
 get { return data[index]; }
 set
 {
 if (value is PayrollData)
 data[index] = (PayrollData)value; }
}
```

```
#endregion
```

```
#region ICollection Members
```

```
public void CopyTo(Array array, int index)
{ (data as System.Collections.ICollection).
CopyTo(array, index); }
```

```
public int Count { get { return data.Count; } }
```

```
public bool IsSynchronized
{ get { return data as
System.Collections.ICollection).IsSynchronized;}}
```

```
public object SyncRoot
{ get { return (data as
System.Collections.ICollection).SyncRoot; } }
```

```
#endregion
```

```
#region IEnumerable Members
```

```
public System.Collections.IEnumerator GetEnumerator()
{ return data.GetEnumerator(); }
```

```
#endregion
```

```
public void SafeUpdate(IEnumerable<PayrollData>
bindingList)
{
 // make the copy:
 BindingList<PayrollData> updates =
 new BindingList<PayrollData>(bindingList.ToList()));
```