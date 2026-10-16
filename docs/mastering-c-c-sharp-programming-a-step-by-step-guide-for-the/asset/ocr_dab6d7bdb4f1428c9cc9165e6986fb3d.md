```
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

In this, we use the -> operator for accessing fields and to invoke struct methods though pointers. Because P->I is the exact equivalent of (*P).I, we could have written the Main method like this:

```
class Test
{
```