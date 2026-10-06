# 224 CHAPTER 7 EXTENDING LINQ TO OBJECTS

```
{
  if (elements.Length == count)
    Array.Resize(ref elements, count * 2);

  elements[count++] = element;
}
```

```
public IEnumerator<TElement> GetEnumerator()
{
  for (int i = 0; i < count; i++)
    yield return elements[i];
}
```

```
IEnumerator IEnumerable.GetEnumerator()
{
  return GetEnumerator();
}
```

```
TKey IGrouping<TKey, TElement>.Key
{
  get { return key; }
}
```

```
int ICollection<TElement>.Count
{
  get { return count; }
}
```

```
bool ICollection<TElement>.IsReadOnly
{
  get { return true; }
}
```

```
void ICollection<TElement>.Add(TElement item)
{
  throw new NotSupportedException();
}
```

```
void ICollection<TElement>.Clear()
{
  throw new NotSupportedException();
}
```

```
bool ICollection<TElement>.Contains(TElement item)
{
```