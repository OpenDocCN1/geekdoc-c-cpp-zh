```
}
public static int getX() {
    return x;
}
}
class StaticTester {
    static void Main(string[] args) {
        StaticVariable var = new StaticVariable();

        var.count();
        var.count();
        var.count();
        Console.WriteLine("Variable x is: {0}", StaticVariable.getX());
        Console.ReadKey();
    }
}
}
```

The code will return the following:

![](bbox=[0.052, 0.51, 0.866, 0.599])