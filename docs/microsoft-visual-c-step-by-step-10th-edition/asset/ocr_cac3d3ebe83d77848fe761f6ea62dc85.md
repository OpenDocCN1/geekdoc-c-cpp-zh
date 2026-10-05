```
class TextReader
{
    ...
    public virtual void Close()
    {
        ...
    }
}

class Example
{
    void Use()
    {
        TextReader reader = ...;
        // use reader
        reader.Close();
    }
}
```