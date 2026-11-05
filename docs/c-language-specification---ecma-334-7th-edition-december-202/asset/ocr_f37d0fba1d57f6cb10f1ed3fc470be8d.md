```
int Count { get; }
bool IsReadOnly { get; }
void Add(T item);
void Clear();
bool Contains(T item);
void CopyTo(T[] array, int arrayIndex);
bool Remove(T item);
}

public interface IEnumerable<T> : IEnumerable
{
    IEnumerator<T> GetEnumerator();
}

public interface IEnumerator<T> : IDisposable, IEnumerator
{
    T Current { get; }
}

public interface IList<T> : ICollection<T>
{
    T this [int index] { get; set; }
    int IndexOf(T item);
    void Insert(int index, T item);
    void RemoveAt(int index);
}

public interface IReadOnlyCollection<out T> : IEnumerable<T>
{
    int Count { get; }
}

public interface IReadOnlyList<out T> : IReadOnlyCollection<T>
{
    T this [int index] { get; }
}

namespace System.Diagnostics
{
    [AttributeUsageAttribute(AttributeTargets.Method | AttributeTargets.Class,
    AllowMultiple = true)]
    public sealed class ConditionalAttribute : Attribute
    {
        public ConditionalAttribute(string conditionString);
        public string ConditionString { get; }
    }
}

namespace System.Reflection
{
    public abstract class MemberInfo
    {
        protected MemberInfo();
    }
}
```