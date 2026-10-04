Instances of anonymous types are not supposed to leak outside of a method. A method cannot be prototyped as an anonymous type because there is no way to specify the anonymous type. Similarly, a method cannot indicate that it returns a reference to an anonymous type. Although it is possible to treat an instance of an anonymous type as an Object (because all anonymous types are derived from Object), there is no way to cast a variable of type Object back into an anonymous type because you don't know the name of the anonymous type at compile. If you want to pass a tuple around, then you should consider using the System.Tuple type discussed in the next section.

# The System.Tuple Type

In the System namespace, Microsoft has several generic Tuple types (all derived from Object) that differ by arity (the number of generic parameters). Here is what the simplest and most complex ones essentially look like.

```
// This is the simplest:
[Serializable]
public class Tuple<T1> {
    private T1 m_item1;
    public Tuple(T1 item1) { m_item1 = item1; }
    public T1 Item1 { get { return m_item1; }
}

// This is the most complex:
[Serializable]
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest> {
    private T1 m_item1; private T2 m_item2; private T3 m_item3; private T4 m_item4;
    private T5 m_item5; private T6 m_item6; private T7 m_item7; private TRest m_Rest;

    public Tuple(T1 item1, T2 item2, T3 item3, T4 item4, T5 item5, T6 item6, T7 item7, TRest rest) {
        m_item1 = item1; m_item2 = item2; m_item3 = item3; m_item4 = item4;
        m_item5 = item5; m_item6 = item6; m_item7 = item7; m_Rest = rest;
    }

    public T1 Item1 { get { return m_item1; }
    public T2 Item2 { get { return m_item2; }
    public T3 Item3 { get { return m_item3; }
    public T4 Item4 { get { return m_item4; }
    public T5 Item5 { get { return m_item5; }
    public T6 Item6 { get { return m_item6; }
    public T7 Item7 { get { return m_item7; }
    public TRest Rest { get { return m_Rest; }
n}
```