```
```csharp
{
    Triangle t = new Triangle();
    int area;
    t.setbase(4);
    t.setheight(5);
    area = t.getValue();

    //Display the area
    Console.WriteLine("Area is:{0}", t.getValue());
    Console.WriteLine("Total Paint cost is:{0}", t.amount());
    Console.Read();
}
}
```
```

**When the code is compiled and executed, the output is:**

```
Area is: 10
Total Pain cost is: 500
```