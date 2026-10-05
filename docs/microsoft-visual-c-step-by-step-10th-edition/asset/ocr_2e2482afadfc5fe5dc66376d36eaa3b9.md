```
struct Wrapper
{
    private int[] data;
    ...
    public int[] Data
    {
        get => this.data;
        set => this.data = value;
    }
}
```