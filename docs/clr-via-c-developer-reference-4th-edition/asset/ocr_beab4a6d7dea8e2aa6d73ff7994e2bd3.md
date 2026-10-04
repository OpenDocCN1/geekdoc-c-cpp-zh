```
// Method called after all key/value objects have been deserialized
public virtual IDerializationCallback.OnDeserialization(Object sender) {
    if (m_siInfo == null) return; // Never set, return

    Int32 num = m_siInfo.GetInt32("Version");
    Int32 num2 = m_siInfo.GetInt32("HashSize");
    m_comparer = (IComparer<TKey>)m_siInfo.GetValue("Comparer", typeof(IComparer<TKey>));
    if (num != 0) {
        m_buckets = new Int32[num];
        for (Int32 i = 0; i < m_buckets.Length; i++) m_buckets[i] = -1;
        m_entries = new Entry<TKey, TValue>[num2];
        m_free_list = -1;
        KeyValuePair<TKey, TValue>[] pairArray = (KeyValuePair<TKey, TValue>[])m_siInfo.GetValue("KeyValuePairs", typeof(KeyValuePair<TKey, TValue>[]>
        if (pairArray == null)
            ThrowHelper.ThrowSerializationException("Resource.Serialization.MissingKeys");
        for (Int32 j = 0; j < pairArray.Length; j++) {
            if (pairArray[j].Key == null)
                ThrowHelper.ThrowSerializationException("Resource.Serialization.NullKey");
            Insert(pairArray[j].Key, pairArray[j].Value, true);
        }
    } else {
        m_buckets = null;
    }
    m_version = num;
    m_siInfo = null;
}
```

Each AddValue method takes a String name and some data. Usually, the data is of a simple value like Boolean, Char, Byte, SByte, Int16, UInt16, Int32, UInt64, Double, Decimal, or DateTime. However, you can also call AddValue, passing a reference to an Object as a String. After GetDataObject has added all of the necessary serialization information, it returns to the formatter.

> Note You should always call one of the overloaded AddValue methods to serialize information for your type. If a field implements the ISerializable interface, don't call the GetDataObject on the field. Instead, call AddValue to the field; the formatter will see that the field implements ISerializable and the formatter will call GetDataObject for you. If you were to call GetDataObject on the field object, the formatter wouldn't need to create a new object when deserializing the stream.