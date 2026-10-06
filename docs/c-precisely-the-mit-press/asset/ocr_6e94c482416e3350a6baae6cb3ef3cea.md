# Classes 53

Example 66 Property Used to Access a Log
Class Log implements a simple log that stores the SIZE strings written to it. The static property InstanceCount is the total number of Log objects created. Property Count is the number of log entries written to this log. Property Last is the latest string logged to this log. It has a set- as well as get-accessors, so one can use assignment operators over log.Last += "...". All returns an array of the (up to) SIZE strings created. Example 103 uses these properties. Example 199 shows how to declare automatically implemented properties Count and InstanceCount instead.

```
public class Log {
    private static int instanceCount = 0;
    private int count = 0;
    private String[] log = new String[SIZE];
    public Log() { instanceCount++; }
    public static int InstanceCount { get { return instanceCount; }}
    public void Add(String msg) { log[count++ % SIZE] = msg; }
    public int Count { get { return count; }
    public String Last {
        get { // Returns the last log entry, or null if not logged yet
            return count==0 ? null : log[(count-1)%SIZE];
        }
        set { // Updates the log entry, or creates one if not logged yet
            if (count==0)
                log[count++] = value;
            else
                log[(count-1)%SIZE] = value;
        }
    }
    public String[] All { ... }
}
```

Example 67 Sparse Matrix Indexing
A sparse matrix has many zeros. A sparse matrix may be represented as an array of columns, where each column is an array list (section 27.6) of only the non-zero elements. Using a two-argument index, one can get and set its elements as A[i,j], as if it were one rectangular array. The indexer performs a linear search of column j for the element index i; this may surprise users because the array-like notation suggests constant time.

```
public double this(int i, int j) {
    get {
        List<NonZero> col = this[j];
        int k = 0;
        while (k < col.Count && col[k].i < i)
            k++;
        return k < col.Count && col[k].i == i ? col[k].Mij : 0.0;
    }
    set { ... }
}
```