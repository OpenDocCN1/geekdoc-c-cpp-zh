```
{
    private int seconds;

    public int Seconds
    {
        get
        {
            return seconds;
        }
        set
        {
            seconds = value;
        }
    }

    public int Minutes
    {
        get
        {
            return seconds / 60;
        }
    }
}
```

What we have here is an instance variable named seconds and, with it, a property named Seconds. Just a note - it is very common to use