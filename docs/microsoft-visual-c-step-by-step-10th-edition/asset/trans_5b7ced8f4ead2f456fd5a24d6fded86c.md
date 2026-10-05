

```c
struct Person : IComparable<Person>
{
    public string Name;

    public int CompareTo(Person other)
    {
        return this.Name.CompareTo(other.Name);
    }
}
```

```c
var personList = new Span<Person>(new Person[10]);
personList[0] = new Person() { Name = "John" };
personList[1] = new Person() { Name = "Diana" };
...
```

```c
personList.Sort(); // 在 Span<T> 对象中对数据进行就地排序
int item = personList.BinarySearch(new Person() { Name = "Diana" });
```

```c
Span<byte> chunk = stackalloc byte[1000];
```

```c
public static int Sum(Span<byte> block)
{
    int sum = 0;
    foreach(byte b in block)
    {
        sum += b;
    }
    return sum;
}
```

```c
interface IWrapper<T>
{
    void SetData(T data);
    T GetData();
}

class Wrapper<T> : IWrapper<T>
{
    private T storedData;

    void IWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }

    T IWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
```

```c
Wrapper<string> stringWrapper = new Wrapper<string>();
IWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
Console.WriteLine($"Stored value is {storedStringWrapper.GetData()}");
```

```c
IWrapper<object> storedObjectWrapper = stringWrapper;
```

```c
IWrapper<object> storedObjectWrapper = (IWrapper<object>)stringWrapper;
```

```c
IWrapper<object> storedObjectWrapper = (IWrapper<object>)stringWrapper;
Circle myCircle = new Circle();
storedObjectWrapper.SetData(myCircle);
```

```c
interface IStoreWrapper<T>
{
    void SetData(T data);
}

interface IRetrieveWrapper<T>
{
    T GetData();
}

class Wrapper<T> : IStoreWrapper<T>, IRetrieveWrapper<T>
{
    private T storedData;

    void IStoreWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }

    T IRetrieveWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
```

```c
Wrapper<string> stringWrapper = new Wrapper<string>();
IStoreWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
IRetrieveWrapper<string> retrievedStringWrapper = stringWrapper;
Console.WriteLine($"Stored value is {retrievedStringWrapper.GetData()}");
```

```c
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

```c
interface IRetrieveWrapper<out T>
{
    T GetData();
}
```

```c
// string 派自 object，所以这是合法的
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

```c
Wrapper<int> intWrapper = new Wrapper<int>();
IStoreWrapper<int> storedIntWrapper = intWrapper; // 这是合法的
// 以下语句是不合法的 - int 不是对象
IRetrieveWrapper<object> retrievedObjectWrapper = intWrapper;
```

```c
interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

```c
class ObjectComparer : IComparer<Object>
{
    int IComparer<Object>.Compare(Object x, Object y)
    {
        int xHash = x.GetHashCode();
        int yHash = y.GetHashCode();
        if (xHash == yHash) return 0;
        if (xHash < yHash) return -1;
        return 1;
    }
}
```

```c
Object x = ...;
Object y = ...;
IComparer<Object> comparer = new ObjectComparer();
int result = comparer.Compare(x, y);
```

