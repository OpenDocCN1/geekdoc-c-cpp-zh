```
```csharp
public override String Message {
    get {
        String baseMsg = base.Message;
        return (m_args == null) ? baseMsg : baseMsg + " (" + m_args.Message + ")";
    }
}

public override Boolean Equals(Object obj) {
    Exception<TExceptionArgs> other = obj as Exception<TExceptionArgs>;
    if (other == null) return false;
    return Object.Equals(m_args, other.m_args) && base.Equals(obj);
}
public override int GetHashCode() { return base.GetHashCode(); }
}
```
```

And the ExceptionArgs base class that TExceptionArgs is constrained to is very simple and looks like this.

```
```csharp
[Serializable]
public abstract class ExceptionArgs {
    public virtual String Message { get { return String.Empty; } }
}
```
```

Now, with these two classes defined, I can trivially define more exception classes when I need to. To define an exception type indicating the disk is full, I simply do the following.

```
```csharp
[Serializable]
public sealed class DiskFullExceptionArgs : ExceptionArgs {
    private readonly String m_diskpath; // private field set at construction time

    public DiskFullExceptionArgs(String diskpath) { m_diskpath = diskpath; }

    // Public read-only property that returns the field
    public String DiskPath { get { return m_diskpath; } }

    // Override the Message property to include our field (if set)
    public override String Message {
        get {
            return (m_diskpath == null) ? base.Message : "DiskPath=" + m_diskpath;
        }
    }
}
```
```

And, if I have no additional data that I want to put inside the class, it gets as simple as the following.

```
```csharp
[Serializable]
public sealed class DiskFullExceptionArgs : ExceptionArgs { }
```
```